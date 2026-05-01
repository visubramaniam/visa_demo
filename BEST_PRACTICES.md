# NVMe/TCP Best Practices for Enterprise Storage

Industry-standard design guidelines for NVMe over TCP deployments with enterprise block storage arrays, with specific recommendations for Hitachi Vantara VSP One Block systems.

---

## 1. NVM Subsystem Design

### Subsystem-to-Host Ratio

| Pattern | Ratio | When to Use |
|---------|-------|-------------|
| **1:1** (one subsystem per host) | Recommended | Default for most deployments. Provides namespace security isolation, independent host mode settings, and per-host firmware/patching flexibility. |
| **1:N** (one subsystem, many hosts) | Acceptable | Shared-nothing clusters (e.g., database replicas) where all hosts need identical namespace access and use the same OS host mode. |
| **N:1** (many subsystems per host) | Avoid | Adds management complexity with no performance benefit. Use a single subsystem with more namespaces instead. |

**Recommendation:** Use one NVM subsystem per host (or per host pair in active/passive HA). This aligns with NVMe-oF spec guidance and ensures clean namespace security boundaries.

### Subsystem Naming Convention

Use a consistent, discoverable naming scheme:

```
NVMeTCP_<OS>_<ArrayModel>_<HostIdentifier>
```

Examples:
- `NVMeTCP_RHEL_VSPOneB28` — RHEL host
- `NVMeTCP_ESXi_VSPOneB28` — ESXi host
- `NVMeTCP_RHEL_VSPOneB28_db01` — specific database server

### Host Mode Selection

| OS | Host Mode | Notes |
|----|-----------|-------|
| RHEL / SUSE / Oracle Linux | LINUX/IRIX | Standard Linux NVMe initiator |
| VMware ESXi | VMWARE_EX | Required for ESXi VAAI and namespace visibility |
| Windows Server | WIN_EX | Windows NVMe initiator |

---

## 2. Storage Ports and Network Topology

### Subsystem Port Count

| Metric | Recommendation | Rationale |
|--------|---------------|-----------|
| **Minimum ports per subsystem** | 2 | Provides path redundancy for failover. Single-port = single point of failure. |
| **Recommended ports per subsystem** | 2–4 | 2 ports for standard workloads; 4 ports for bandwidth-intensive workloads (video, analytics). |
| **Maximum ports per subsystem** | 8 | Diminishing returns beyond 8. The NVMe multipath layer can struggle with excessive path counts. |

### Port-to-Fabric Mapping

**Critical rule:** Each subsystem port should reside on a **separate physical fabric or network segment** for true redundancy.

```
Fabric A (VLAN 10)          Fabric B (VLAN 20)
┌──────────┐                ┌──────────┐
│  CL1-D   │                │  CL2-D   │
│ (Port 1) │                │ (Port 2) │
│ 10.0.1.30│                │ 10.0.2.30│
└────┬─────┘                └────┬─────┘
     │                           │
     │    ┌─────────────┐        │
     └────┤  Host NIC 1 │────────┘
          │  Host NIC 2 │
          └─────────────┘
```

| Ports | Fabrics | Configuration |
|-------|---------|--------------|
| 2 ports | 2 fabrics | **Standard** — 1 port per fabric. Full redundancy. |
| 4 ports | 2 fabrics | **High bandwidth** — 2 ports per fabric. Redundancy + throughput. |
| 4 ports | 4 fabrics | **Maximum isolation** — 1 port per fabric. Best fault domain separation. |

### Port Speed Alignment

| Host NIC Speed | Storage Port Speed | Notes |
|---------------|-------------------|-------|
| 25 GbE | 25 GbE | Matched; no bottleneck |
| 100 GbE | 100 GbE | **Recommended** for NVMe/TCP |
| 100 GbE | 25 GbE | Storage-side bottleneck; use 4 storage ports to compensate |
| 10 GbE | 25/100 GbE | Acceptable for low-IOPS workloads only |

---

## 3. Namespace and LDEV Sizing

### Namespace-to-Subsystem Ratio

| Namespace Count | Use Case | Notes |
|----------------|----------|-------|
| 1–10 | Standard databases, file servers | Simple, easy to manage |
| 10–64 | Virtualization (ESXi datastores), multi-tenant | Common in production |
| 64–256 | Large-scale VDI, container storage | Monitor discovery time |
| 256+ | Avoid | Discovery overhead increases; most implementations limit to 256–1024 per subsystem (the NVMe base spec defines NSID as a 32-bit value with a far higher theoretical maximum; the 256–1024 figures are vendor implementation limits, not spec limits) |

**Recommended starting point:** 10 namespaces per subsystem (as used in this project).

### Namespace-to-Port Path Ratio

Every namespace is accessible through **every port** assigned to the subsystem. This means:

```
Total paths = Namespaces × Ports
```

| Namespaces | Ports | Total Paths | Assessment |
|-----------|-------|-------------|------------|
| 10 | 2 | 20 | Optimal |
| 10 | 4 | 40 | Good — high bandwidth scenarios |
| 64 | 2 | 128 | Acceptable |
| 64 | 4 | 256 | Monitor — high path count |
| 256 | 4 | 1024 | Caution — path management overhead |

**Rule of thumb:** Keep total paths (namespaces x ports) under 256 per host for predictable performance. Above 512 paths, multipath discovery and failover times increase noticeably.

### LDEV Sizing

| Workload | LDEV Size | Rationale |
|----------|-----------|-----------|
| Database (OLTP) | 50–200 GB | Match tablespace/data file size for granular management |
| Database (OLAP/DW) | 200 GB – 2 TB | Larger volumes reduce management overhead |
| VMware datastores | 1–4 TB | VMware recommends max 64 TB per datastore |
| General file storage | 500 GB – 2 TB | Balance between management and utilization |
| Test/Dev | 10–50 GB | Small volumes for quick provisioning |

---

## 4. NVMe/TCP Network Configuration

### Dedicated Storage Network

| Practice | Priority |
|----------|----------|
| Use dedicated VLANs for NVMe/TCP traffic | **Required** |
| Separate storage VLANs from management/vMotion | **Required** |
| Use jumbo frames (MTU 9000) | **Recommended** |
| Disable spanning tree on storage ports (portfast) | **Recommended** |
| Enable flow control (PFC or global pause) | **Optional — evaluate based on environment** (see note below) |

> **Flow control note:** PFC (Priority Flow Control / 802.1Qbb) is a hard requirement for lossless RoCEv2 fabrics, **not** NVMe/TCP. Deploying PFC for TCP-based storage adds significant switch configuration complexity (DCBX, ETS, PFC watchdog) with minimal benefit, since TCP natively handles congestion and retransmission. Global pause (802.3x) can reduce TCP retransmits under burst conditions but is a blunt instrument that risks head-of-line blocking across all traffic classes on a port. For NVMe/TCP, proper TCP tuning (buffer sizes, SACK, window scaling) is the primary performance lever. Evaluate flow control only if burst-induced retransmits are confirmed by measurement.

### IP Addressing

- Use **/24 subnets** minimum for storage networks
- Keep each fabric on a **separate subnet** (e.g., 192.168.10.0/24 and 192.168.20.0/24)
- Use **static IPs** on both host NICs and storage ports — no DHCP for storage traffic
- Assign one host NIC per storage subnet for deterministic path routing

### TCP Tuning (Linux)

```bash
# Increase socket buffer sizes for NVMe/TCP
sysctl -w net.core.rmem_max=4194304
sysctl -w net.core.wmem_max=4194304
sysctl -w net.ipv4.tcp_rmem="4096 87380 4194304"
sysctl -w net.ipv4.tcp_wmem="4096 65536 4194304"

# SACK — critical for efficient retransmit recovery on storage networks
sysctl -w net.ipv4.tcp_sack=1

# Timestamps — required for accurate RTT measurement at high throughput
sysctl -w net.ipv4.tcp_timestamps=1

# Low-latency mode — where supported, prioritizes latency over throughput aggregation
sysctl -w net.ipv4.tcp_low_latency=1

# Persist in /etc/sysctl.d/99-nvme-tcp.conf
# For latency-sensitive workloads, also consider setting TCP_QUICKACK at the
# application level or reducing delayed ACK via tcp_delack_min.
```

### Firewall Rules

| Port | Protocol | Direction | Purpose |
|------|----------|-----------|---------|
| 8009 | TCP | Host → Storage | NVMe discovery |
| 4420 | TCP | Host → Storage | NVMe I/O (data) |

---

## 5. Multipathing

### NVMe Native Multipath vs. DM-Multipath

| Feature | NVMe Native Multipath | DM-Multipath (multipathd) |
|---------|----------------------|--------------------------|
| Kernel support | Built-in (4.15+, production-quality from 5.x; RHEL 8's backported 4.18 kernel includes multipath fixes not present in upstream 4.18 — the version number alone can be misleading) | Requires daemon |
| Namespace presentation | Single `/dev/nvmeXnY` per namespace | `/dev/dm-X` mapper device |
| IO policy | round-robin, numa | round-robin, queue-length, service-time |
| Overhead | Minimal (kernel-level) | Higher (userspace daemon) |
| NVMe-oF awareness | Full | Limited |
| **Recommendation** | **Use this** for NVMe/TCP | Legacy FC/iSCSI only |

**Do NOT mix both.** Disable `multipathd` and remove `/etc/multipath.conf` when using NVMe native multipath.

### Enabling NVMe Native Multipath (Linux)

```bash
# Set on ALL kernels (survives kernel upgrades)
grubby --args=nvme_core.multipath=Y --update-kernel ALL

# Belt-and-suspenders: also set via modprobe
echo "options nvme_core multipath=Y" > /etc/modprobe.d/nvme_core.conf

# Rebuild initramfs
dracut -f

# Reboot required
```

**Important:** Use `--update-kernel ALL`, not `--update-kernel /boot/vmlinuz-$(uname -r)`. The latter only applies to the running kernel and will be lost when the system boots a newer kernel after package updates.

### IO Policy

| Policy | Use Case |
|--------|----------|
| **round-robin** | Default. Best for uniform path latency (same fabric type, same hop count). |
| **numa** | Multi-socket servers where NUMA-local paths reduce cross-socket traffic. |

Set via udev rule for persistence:

```bash
# /etc/udev/rules.d/71-nvme-io-policy.rules
ACTION=="add|change", SUBSYSTEM=="nvme-subsystem", \
  ATTRS{model}=="HITACHI*", ATTR{iopolicy}="round-robin"
```

### Path Verification

After configuration, verify:

```bash
# Multipath enabled
cat /sys/module/nvme_core/parameters/multipath
# Expected: Y

# IO policy active
cat /sys/class/nvme-subsystem/nvme-subsys*/iopolicy
# Expected: round-robin

# Path count (should show multiple transports per subsystem)
nvme list-subsys
# Expected: 2+ paths per subsystem, all "live"
```

---

## 6. Discovery and Connection

### Discovery Controller

| Practice | Detail |
|----------|--------|
| Use persistent discovery via `/etc/nvme/discovery.conf` | Survives reboots |
| Enable `nvmf-autoconnect.service` | Auto-reconnects on boot and after network recovery |
| Discover through **each fabric separately** | Ensures all paths are found |

### Connection Method

| Method | Recommendation |
|--------|---------------|
| `nvme connect-all` | Preferred on modern kernels (5.x+) with nvme-cli 2.x+. Single command discovers and connects all. |
| `nvme connect` (explicit per-port) | **Required** for older kernels (4.18.x) or nvme-cli 1.x. More reliable and debuggable. |

For RHEL 8 (kernel 4.18, nvme-cli 1.16):

```bash
# Explicit connect per storage port
nvme connect -t tcp -n <subsystem_nqn> \
  -a <storage_port_ip> -s 4420 \
  -w <host_nic_ip>
```

### Autoconnect Service

```bash
systemctl enable --now nvmf-autoconnect.service
```

This reads `/etc/nvme/discovery.conf` on boot and re-establishes connections.

---

## 7. Performance Tuning

### Queue Depth

| Parameter | Default | Tuned | Notes |
|-----------|---------|-------|-------|
| `nr_io_queues` | CPU count | CPU count or less | One queue per CPU core; reduce if many namespaces compete |
| `queue_size` | 128 | 128–1024 | Increase for sequential workloads; monitor memory usage |
| `keep_alive_tmo` | 30 (sec, implementation-specific — some kernels/controllers negotiate a different value; 5 s has been observed on certain setups but is not the universal default) | 30–60 | Increase in lossy networks to avoid false path failures; avoid very short values as they generate frequent keep-alive probes |

### Workload-Specific Guidance

| Workload | Queue Depth | IO Scheduler | Block Size |
|----------|-------------|-------------|------------|
| OLTP Database | 32–64 | none (bypass) | 4K–8K |
| OLAP / Analytics | 128–256 | none | 64K–256K |
| VMware Datastores | 32 (per device) | N/A (ESXi managed) | 1 MB (VMFS) |
| File Server | 64–128 | mq-deadline | 4K |

### IO Scheduler for NVMe

```bash
# NVMe devices should use 'none' (passthrough) scheduler
echo none > /sys/block/nvme0n1/queue/scheduler

# Persist via udev
ACTION=="add|change", KERNEL=="nvme*", ATTR{queue/scheduler}="none"
```

---

## 8. Monitoring and Troubleshooting

### Key Health Checks

```bash
# List all NVMe namespaces with capacity and firmware
nvme list

# Show subsystem topology and path status
nvme list-subsys

# Check for errors on a specific device
nvme smart-log /dev/nvme0n1

# Verify multipath status
cat /sys/module/nvme_core/parameters/multipath

# Check IO policy
cat /sys/class/nvme-subsystem/nvme-subsys*/iopolicy

# Monitor NVMe/TCP connections
ss -tnp | grep :4420
```

### Common Issues

| Symptom | Likely Cause | Fix |
|---------|-------------|-----|
| `nvme connect` returns "Invalid argument" | `--ctrl-loss-tmo=-1` not supported on kernel 4.18 | Remove the flag; use default timeout |
| `nvme connect-all` fails silently | nvme-cli 1.x incompatibility | Use explicit `nvme connect` per port |
| Multipath shows `N` after reboot | `grubby` only set on old kernel | Use `--update-kernel ALL` + `/etc/modprobe.d/nvme_core.conf` |
| 20 devices instead of 10 | Multipath disabled; each path appears as separate device | Enable `nvme_core.multipath=Y` and reboot |
| Discovery finds 0 records | Firewall blocking port 8009 or 4420 | Open ports; verify with `ping` and `ss` |
| Connection drops after idle | `keep_alive_tmo` too short | Increase to 30s; check network stability |
| Paths show `connecting` not `live` | Network issue or storage port down | Check cables, switch, storage port status |

---

## 9. Capacity Planning Reference

### Scaling Guidelines

| Component | Small (Dev/Test) | Medium (Production) | Large (Enterprise) |
|-----------|-----------------|--------------------|--------------------|
| Hosts per array | 1–4 | 4–16 | 16–64 |
| Subsystems per array | 1–4 | 4–16 | 16–64 |
| Namespaces per subsystem | 1–10 | 10–64 | 64–256 |
| Ports per subsystem | 2 | 2–4 | 4–8 |
| Total paths per host | 2–20 | 20–128 | 128–512 |
| LDEVs per array | 10–50 | 50–500 | 500–4096 |

### VSP One Block 28 Specific Limits

| Resource | Maximum |
|----------|---------|
| NVM Subsystems | 64 |
| Namespaces per subsystem | 256 |
| Ports per subsystem | 8 |
| Host NQNs per subsystem | 32 |
| Total NVMe/TCP ports | Depends on CL card config |

---

## 10. Security

### Namespace Security

- **Enable namespace security** on all production subsystems (default on VSP One Block)
- This ensures only registered host NQNs can access namespaces within the subsystem
- Each host NQN should have a descriptive nickname for audit trails

### Network Isolation

| Layer | Control |
|-------|---------|
| L2 | Dedicated VLANs per storage fabric |
| L3 | ACLs restricting access to storage subnets |
| Firewall | Allow only ports 4420 and 8009 from host IPs |
| Physical | Dedicated NICs (not shared with management/application traffic) |

### TLS (NVMe/TCP 1.1+)

NVMe/TCP supports in-band TLS (NVMe-TCP specification 1.1). When available:
- Use TLS 1.3 for encryption of data in transit
- Deploy per-host certificates for mutual authentication
- Note: TLS adds approximately 5–10% **throughput** overhead on hosts with AES-NI hardware offload; latency impact for small-block IOPS (e.g., 4K random reads in OLTP workloads) can be proportionally higher, particularly on hosts without AES-NI or at very high IOPS rates where per-PDU encryption cost compounds. Evaluate carefully for latency-sensitive workloads.

---

## Quick Reference: This Project's Configuration

| Component | ESXi Setup | RHEL Setup |
|-----------|-----------|------------|
| NVM Subsystem | NVMeTCP_VSPOneB28 (ID: 0) | NVMeTCP_RHEL_VSPOneB28 (ID: 1) |
| Host Mode | VMWARE_EX | LINUX/IRIX |
| Storage Ports | CL1-D, CL2-D | CL3-D, CL4-D |
| LDEVs | 5888–5897 (10 x 10 GB) | 6144–6153 (10 x 10 GB) |
| Namespaces | 10 | 10 |
| Total Paths | 20 (10 ns x 2 ports) | 20 (10 ns x 2 ports) |
| Multipath | ESXi native (HPP) | NVMe native (`nvme_core.multipath=Y`) |
| IO Policy | Round Robin | Round Robin (udev rule) |
| Connect Method | `esxcli nvme connect` | `nvme connect` (explicit per-port) |
