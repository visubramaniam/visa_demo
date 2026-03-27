# NVMe/TCP End-to-End Ansible Playbook Output

**Command:** `ansible-playbook site.yml`
**Result:** SUCCESS (ok=35, changed=5, failed=0)

---

## Step 1: Create LDEVs for NVMe/TCP Namespaces

10 LDEVs created (IDs 5888–5897), each 10 GB.

| LDEV ID | Status |
|---------|--------|
| 5888 | ok |
| 5889 | ok |
| 5890 | ok |
| 5891 | ok |
| 5892 | ok |
| 5893 | ok |
| 5894 | ok |
| 5895 | ok |
| 5896 | ok |
| 5897 | ok |

---

## Step 2: Create NVM Subsystem with Ports and Host NQN

**Status:** changed

### NVM Subsystem Info

| Property | Value |
|----------|-------|
| Name | NVMeTCP_VSPOneB28 |
| ID | 0 |
| Host Mode | VMWARE_EX |
| Namespace Security | Enable |
| T10PI Mode | Disable |
| Storage Serial | 840498 |

### Ports

| Port ID | Port Type |
|---------|-----------|
| CL1-D | NVME_TCP |
| CL2-D | NVME_TCP |

### Host NQN

| NQN | Nickname |
|-----|----------|
| `nqn.2014-08.org.nvmexpress:uuid:69bbe589-c966-e3d0-2780-d8c497808757` | esxi_host_nqn |

### Namespace Paths (10 paths)

| Namespace ID | LDEV ID | LDEV Hex |
|--------------|---------|----------|
| 1 | 5888 | 00:17:00 |
| 2 | 5889 | 00:17:01 |
| 3 | 5890 | 00:17:02 |
| 4 | 5891 | 00:17:03 |
| 5 | 5892 | 00:17:04 |
| 6 | 5893 | 00:17:05 |
| 7 | 5894 | 00:17:06 |
| 8 | 5895 | 00:17:07 |
| 9 | 5896 | 00:17:08 |
| 10 | 5897 | 00:17:09 |

### Namespaces (10 x 10 GB)

| Namespace ID | LDEV ID | Capacity | Nickname |
|--------------|---------|----------|----------|
| 1 | 5888 | 10.00GB | nvme_tcp_ldev_ns_5888 |
| 2 | 5889 | 10.00GB | nvme_tcp_ldev_ns_5889 |
| 3 | 5890 | 10.00GB | nvme_tcp_ldev_ns_5890 |
| 4 | 5891 | 10.00GB | nvme_tcp_ldev_ns_5891 |
| 5 | 5892 | 10.00GB | nvme_tcp_ldev_ns_5892 |
| 6 | 5893 | 10.00GB | nvme_tcp_ldev_ns_5893 |
| 7 | 5894 | 10.00GB | nvme_tcp_ldev_ns_5894 |
| 8 | 5895 | 10.00GB | nvme_tcp_ldev_ns_5895 |
| 9 | 5896 | 10.00GB | nvme_tcp_ldev_ns_5896 |
| 10 | 5897 | 10.00GB | nvme_tcp_ldev_ns_5897 |

### Auto-Generated Subsystem NQN

```
nqn.1994-04.jp.co.hitachi:nvme:storage-subsystem-sn.8-40498-nvmssid.00000
```

---

## Step 3: Add Namespaces and Namespace Paths

**Status:** changed (all 10 namespaces)

| LDEV ID | Status |
|---------|--------|
| 5888 | added |
| 5889 | added |
| 5890 | added |
| 5891 | added |
| 5892 | added |
| 5893 | added |
| 5894 | added |
| 5895 | added |
| 5896 | added |
| 5897 | added |

---

## Step 4: Configure ESXi Networking

| Task | Status |
|------|--------|
| Create vSwitch1 (first 100G NIC) | ok |
| Create vSwitch2 (second 100G NIC) | ok |
| Create portgroup on vSwitch1 | ok |
| Create portgroup on vSwitch2 | ok |
| Create VMkernel adapter 1 on vSwitch1 | ok |
| Create VMkernel adapter 2 on vSwitch2 | ok |
| Tag vmk1 for NVMe/TCP | ok (already tagged) |
| Tag vmk2 for NVMe/TCP | ok (already tagged) |

---

## Step 5: Add NVMe/TCP Software Adapters

| NIC | Status | Message |
|-----|--------|---------|
| vmnic2 | ok | NVMe/TCP already enabled on vmnic2 |
| vmnic3 | ok | NVMe/TCP already enabled on vmnic3 |

### NVMe Adapter List

| Adapter | Adapter Qualified Name | Transport Type | Driver | Associated Device |
|---------|----------------------|----------------|--------|-------------------|
| vmhba64 | aqn:nvmetcp:58-a2-e1-11-dc-4c-T | TCP | nvmetcp | vmnic2 |
| vmhba65 | aqn:nvmetcp:58-a2-e1-11-dc-4d-T | TCP | nvmetcp | vmnic3 |

---

## Step 6: Add NVMe/TCP Target Controllers

**Subsystem NQN:** `nqn.1994-04.jp.co.hitachi:nvme:storage-subsystem-sn.8-40498-nvmssid.00000`

| Storage Port | Status | Message |
|-------------|--------|---------|
| 192.168.52.31:4420 (CL1-D) | ok | Controller already connected |
| 192.168.52.32:4420 (CL2-D) | ok | Controller already connected |

### Connected Controllers

| NQN + Adapter + Target | Controller # | Adapter | Transport | Online | Type | Keep Alive | IO Queues | Queue Size |
|------------------------|-------------|---------|-----------|--------|------|-----------|-----------|------------|
| ...nvmssid.00000#vmhba64#192.168.52.31:4420 | 256 | vmhba64 | TCP | true | I/O | 10 | 4 | 128 |
| ...nvmssid.00000#vmhba65#192.168.52.32:4420 | 257 | vmhba65 | TCP | true | I/O | 10 | 4 | 128 |

### NVMe/TCP Namespaces Visible to ESXi (20 paths = 10 namespaces x 2 controllers)

| EUI | Controller # | Namespace ID | Block Size | Capacity (MB) |
|-----|-------------|--------------|------------|---------------|
| eui.50809e32000000000060e8289e321700 | 256 | 1 | 512 | 10240 |
| eui.50809e32000000000060e8289e321701 | 256 | 2 | 512 | 10240 |
| eui.50809e32000000000060e8289e321700 | 257 | 1 | 512 | 10240 |
| eui.50809e32000000000060e8289e321701 | 257 | 2 | 512 | 10240 |
| eui.50809e32000000000060e8289e321702 | 257 | 3 | 512 | 10240 |
| eui.50809e32000000000060e8289e321702 | 256 | 3 | 512 | 10240 |
| eui.50809e32000000000060e8289e321703 | 257 | 4 | 512 | 10240 |
| eui.50809e32000000000060e8289e321703 | 256 | 4 | 512 | 10240 |
| eui.50809e32000000000060e8289e321704 | 256 | 5 | 512 | 10240 |
| eui.50809e32000000000060e8289e321704 | 257 | 5 | 512 | 10240 |
| eui.50809e32000000000060e8289e321705 | 257 | 6 | 512 | 10240 |
| eui.50809e32000000000060e8289e321705 | 256 | 6 | 512 | 10240 |
| eui.50809e32000000000060e8289e321706 | 256 | 7 | 512 | 10240 |
| eui.50809e32000000000060e8289e321706 | 257 | 7 | 512 | 10240 |
| eui.50809e32000000000060e8289e321707 | 257 | 8 | 512 | 10240 |
| eui.50809e32000000000060e8289e321707 | 256 | 8 | 512 | 10240 |
| eui.50809e32000000000060e8289e321708 | 257 | 9 | 512 | 10240 |
| eui.50809e32000000000060e8289e321708 | 256 | 9 | 512 | 10240 |
| eui.50809e32000000000060e8289e321709 | 256 | 10 | 512 | 10240 |
| eui.50809e32000000000060e8289e321709 | 257 | 10 | 512 | 10240 |

---

## Play Recap

| Host | OK | Changed | Unreachable | Failed | Skipped | Rescued | Ignored |
|------|---:|--------:|------------:|-------:|--------:|--------:|--------:|
| localhost | 35 | 5 | 0 | 0 | 0 | 0 | 0 |
