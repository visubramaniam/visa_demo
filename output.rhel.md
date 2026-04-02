# NVMe/TCP End-to-End Ansible Playbook Output (RHEL)

**Command:** `ansible-playbook site_rhel.yml`
**Result:** SUCCESS (ok=53, changed=10, failed=0, skipped=8)
**Total Duration:** 5 minutes 23 seconds
**Target Host:** 192.168.53.160 (RHEL 8.10, kernel 4.18.0-553.115.1.el8_10.x86_64)

---

## Step 1: Create LDEVs for NVMe/TCP Namespaces

10 LDEVs created (IDs 6144–6153), each 10 GB.

| LDEV ID | Status |
|---------|--------|
| 6144 | ok |
| 6145 | ok |
| 6146 | ok |
| 6147 | ok |
| 6148 | ok |
| 6149 | ok |
| 6150 | ok |
| 6151 | ok |
| 6152 | ok |
| 6153 | ok |

**Duration:** 1m 36s

---

## Step 2: Configure RHEL Networking

### NVMe CLI

| Task | Status | Detail |
|------|--------|--------|
| Verify nvme-cli installed | ok | nvme-cli-1.16-9.el8.x86_64 |
| Install nvme-cli | skipped | Already present |

### Host NQN

```
nqn.2014-08.org.nvmexpress:uuid:ca845a3c-fe2f-4e6a-96dd-99b094774113
```

### NIC Configuration

| NIC | IP Address | Status |
|-----|-----------|--------|
| ens97f1 | 192.168.10.45/24 | changed |
| ens99f1 | 192.168.20.45/24 | changed |

### Storage Port Connectivity

| Storage Port | IP | Status |
|-------------|-----|--------|
| CL3-D | 192.168.10.30 | SUCCESS |
| CL4-D | 192.168.20.30 | SUCCESS |

---

## Step 3: Create NVM Subsystem with Ports and Host NQN

**Status:** changed

### NVM Subsystem Info

| Property | Value |
|----------|-------|
| Name | NVMeTCP_RHEL_VSPOneB28 |
| ID | 1 |
| Host Mode | LINUX/IRIX |
| Namespace Security | Enable |
| T10PI Mode | Disable |
| Storage Serial | 840498 |

### Ports

| Port ID | Port Type |
|---------|-----------|
| CL3-D | NVME_TCP |
| CL4-D | NVME_TCP |

### Host NQN

| NQN | Nickname |
|-----|----------|
| nqn.2014-08.org.nvmexpress:uuid:ca845a3c-fe2f-4e6a-96dd-99b094774113 | rhel_host_nqn |

### Namespace Paths (10 paths)

| Namespace ID | LDEV ID | LDEV Hex |
|--------------|---------|----------|
| 1 | 6144 | 00:18:00 |
| 2 | 6145 | 00:18:01 |
| 3 | 6146 | 00:18:02 |
| 4 | 6147 | 00:18:03 |
| 5 | 6148 | 00:18:04 |
| 6 | 6149 | 00:18:05 |
| 7 | 6150 | 00:18:06 |
| 8 | 6151 | 00:18:07 |
| 9 | 6152 | 00:18:08 |
| 10 | 6153 | 00:18:09 |

### Namespaces (10 x 10 GB)

| Namespace ID | LDEV ID | Capacity | Nickname |
|--------------|---------|----------|----------|
| 1 | 6144 | 10.00GB | rhel_nvme_tcp_ldev_ns_6144 |
| 2 | 6145 | 10.00GB | rhel_nvme_tcp_ldev_ns_6145 |
| 3 | 6146 | 10.00GB | rhel_nvme_tcp_ldev_ns_6146 |
| 4 | 6147 | 10.00GB | rhel_nvme_tcp_ldev_ns_6147 |
| 5 | 6148 | 10.00GB | rhel_nvme_tcp_ldev_ns_6148 |
| 6 | 6149 | 10.00GB | rhel_nvme_tcp_ldev_ns_6149 |
| 7 | 6150 | 10.00GB | rhel_nvme_tcp_ldev_ns_6150 |
| 8 | 6151 | 10.00GB | rhel_nvme_tcp_ldev_ns_6151 |
| 9 | 6152 | 10.00GB | rhel_nvme_tcp_ldev_ns_6152 |
| 10 | 6153 | 10.00GB | rhel_nvme_tcp_ldev_ns_6153 |

### Auto-Generated Subsystem NQN

```
nqn.1994-04.jp.co.hitachi:nvme:storage-subsystem-sn.8-40498-nvmssid.00001
```

**Duration:** 19.4s

---

## Step 4: Add Namespaces and Namespace Paths

**Status:** changed (all 10 namespaces)

| LDEV ID | Status |
|---------|--------|
| 6144 | added |
| 6145 | added |
| 6146 | added |
| 6147 | added |
| 6148 | added |
| 6149 | added |
| 6150 | added |
| 6151 | added |
| 6152 | added |
| 6153 | added |

**Duration:** 2m 31s

---

## Step 5: NVMe/TCP Discovery and Connection

### Kernel Module

| Module | Size | Status |
|--------|------|--------|
| nvme_tcp | 36864 | loaded |
| nvme_fabrics | 24576 | loaded (dependency) |
| nvme_core | 139264 | loaded (dependency) |

### NVMe Discovery

**Subsystem NQN:** `nqn.1994-04.jp.co.hitachi:nvme:storage-subsystem-sn.8-40498-nvmssid.00001`

| Storage Port | Transport | Address | Service ID | Security | Status |
|-------------|-----------|---------|------------|----------|--------|
| CL3-D (Port 0) | tcp/ipv4 | 192.168.10.30 | 4420 | none | discovered |
| CL4-D (Port 1) | tcp/ipv4 | 192.168.20.30 | 4420 | none | discovered |

### NVMe Connect

| Connection | Transport | Target Address | Service ID | Host Address | rc | Status |
|-----------|-----------|---------------|------------|-------------|-----|--------|
| Storage Port 1 (CL3-D) | tcp | 192.168.10.30 | 4420 | 192.168.10.45 | 0 | connected |
| Storage Port 2 (CL4-D) | tcp | 192.168.20.30 | 4420 | 192.168.20.45 | 0 | connected |

### NVMe Namespaces Visible to RHEL (20 paths = 10 namespaces x 2 controllers)

| Node | Serial | Model | Namespace | Capacity | Format | FW Rev |
|------|--------|-------|-----------|----------|--------|--------|
| /dev/nvme0n1 | 8-40498-00001 | HITACHI SVOS-RF-System | 1 | 10.74 GB | 512 B | A3042240 |
| /dev/nvme0n2 | 8-40498-00001 | HITACHI SVOS-RF-System | 2 | 10.74 GB | 512 B | A3042240 |
| /dev/nvme0n3 | 8-40498-00001 | HITACHI SVOS-RF-System | 3 | 10.74 GB | 512 B | A3042240 |
| /dev/nvme0n4 | 8-40498-00001 | HITACHI SVOS-RF-System | 4 | 10.74 GB | 512 B | A3042240 |
| /dev/nvme0n5 | 8-40498-00001 | HITACHI SVOS-RF-System | 5 | 10.74 GB | 512 B | A3042240 |
| /dev/nvme0n6 | 8-40498-00001 | HITACHI SVOS-RF-System | 6 | 10.74 GB | 512 B | A3042240 |
| /dev/nvme0n7 | 8-40498-00001 | HITACHI SVOS-RF-System | 7 | 10.74 GB | 512 B | A3042240 |
| /dev/nvme0n8 | 8-40498-00001 | HITACHI SVOS-RF-System | 8 | 10.74 GB | 512 B | A3042240 |
| /dev/nvme0n9 | 8-40498-00001 | HITACHI SVOS-RF-System | 9 | 10.74 GB | 512 B | A3042240 |
| /dev/nvme0n10 | 8-40498-00001 | HITACHI SVOS-RF-System | 10 | 10.74 GB | 512 B | A3042240 |
| /dev/nvme1n1 | 8-40498-00001 | HITACHI SVOS-RF-System | 1 | 10.74 GB | 512 B | A3042240 |
| /dev/nvme1n2 | 8-40498-00001 | HITACHI SVOS-RF-System | 2 | 10.74 GB | 512 B | A3042240 |
| /dev/nvme1n3 | 8-40498-00001 | HITACHI SVOS-RF-System | 3 | 10.74 GB | 512 B | A3042240 |
| /dev/nvme1n4 | 8-40498-00001 | HITACHI SVOS-RF-System | 4 | 10.74 GB | 512 B | A3042240 |
| /dev/nvme1n5 | 8-40498-00001 | HITACHI SVOS-RF-System | 5 | 10.74 GB | 512 B | A3042240 |
| /dev/nvme1n6 | 8-40498-00001 | HITACHI SVOS-RF-System | 6 | 10.74 GB | 512 B | A3042240 |
| /dev/nvme1n7 | 8-40498-00001 | HITACHI SVOS-RF-System | 7 | 10.74 GB | 512 B | A3042240 |
| /dev/nvme1n8 | 8-40498-00001 | HITACHI SVOS-RF-System | 8 | 10.74 GB | 512 B | A3042240 |
| /dev/nvme1n9 | 8-40498-00001 | HITACHI SVOS-RF-System | 9 | 10.74 GB | 512 B | A3042240 |
| /dev/nvme1n10 | 8-40498-00001 | HITACHI SVOS-RF-System | 10 | 10.74 GB | 512 B | A3042240 |

### NVMe Subsystem Paths

```
nvme-subsys0 - NQN=nqn.1994-04.jp.co.hitachi:nvme:storage-subsystem-sn.8-40498-nvmssid.00001
\
 +- nvme0 tcp traddr=192.168.10.30 trsvcid=4420 host_traddr=192.168.10.45 live
 +- nvme1 tcp traddr=192.168.20.30 trsvcid=4420 host_traddr=192.168.20.45 live
```

---

## Step 6: Configure NVMe Native Multipathing

| Task | Status |
|------|--------|
| Check current multipath status | N (not yet active) |
| Enable multipath via grubby (ALL kernels) | changed |
| Create /etc/modprobe.d/nvme_core.conf | changed |
| Disable DM multipathd | ok (stopped/disabled) |
| Remove /etc/multipath.conf | ok |
| Flush DM multipath maps | ok |
| Create udev rule (round-robin IO policy) | ok |
| Regenerate initramfs (dracut -f) | changed (14.6s) |

**Initramfs:** `/boot/initramfs-4.18.0-553.115.1.el8_10.x86_64.img`

> **NOTE:** A reboot of 192.168.53.160 is required to activate NVMe native multipathing.
> After reboot, verify with:
> - `cat /sys/module/nvme_core/parameters/multipath` should show `Y`
> - `cat /sys/class/nvme-subsystem/nvme-subsys*/iopolicy` should show `round-robin`

---

## Task Timing (Top 20 by Duration)

| Task | Duration |
|------|----------|
| Step 4 - Add namespaces and namespace paths to NVM Subsystem | 2m 31.9s |
| Step 1 - Create LDEVs for NVMe/TCP namespaces | 1m 36.6s |
| Step 3 - Create NVM Subsystem with ports and host NQN | 19.4s |
| Step 6 - Regenerate initramfs | 14.6s |
| Step 2 - Verify connectivity to storage port 1 | 4.2s |
| Step 2 - Verify connectivity to storage port 2 | 4.2s |
| Step 2 - Verify nvme-cli is installed | 2.8s |
| Step 5 - Enable and start nvmf-autoconnect service | 2.0s |
| Step 6 - Create udev rule for Hitachi SVOS round-robin IO policy | 1.8s |
| Step 5 - Configure /etc/nvme/discovery.conf | 1.8s |
| Step 5 - Disconnect any stale NVMe-oF sessions | 1.7s |
| Step 5 - Load nvme_tcp kernel module | 1.7s |
| Step 5 - List connected NVMe namespaces | 1.3s |
| Step 5 - List NVMe subsystem paths | 1.3s |
| Step 6 - Disable DM multipath | 1.2s |
| Step 2 - Configure static IP on NIC interface 1 (ens97f1) | 1.2s |
| Step 2 - Configure static IP on NIC interface 2 (ens99f1) | 1.2s |
| Step 5 - Connect to NVMe subsystem via storage port 1 | 1.2s |
| Step 6 - Enable NVMe native multipath via grubby (ALL kernels) | 1.1s |
| Step 2 - Read host NQN from RHEL host | 1.1s |

---

## Play Recap

| Host | OK | Changed | Unreachable | Failed | Skipped | Rescued | Ignored |
|------|---:|--------:|------------:|-------:|--------:|--------:|--------:|
| localhost | 53 | 10 | 0 | 0 | 8 | 0 | 0 |
