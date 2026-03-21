# NVMe/TCP End-to-End Setup: VSP One Block 28 + VMware ESXi

Ansible automation for configuring NVMe over TCP connectivity between a Hitachi Vantara VSP One Block 28 storage system and a VMware ESXi host with 100Gbps network adapters.

## Overview

This project automates the full NVMe/TCP setup in two phases:

**Phase 1 — Storage Configuration (VSP One Block 28)**
1. Create LDEVs (logical devices) for NVMe/TCP namespaces
2. Create an NVM Subsystem with storage ports and host NQN registration
3. Add namespaces and namespace paths to the NVM Subsystem

**Phase 2 — ESXi Host Configuration**
4. Configure vSwitches and VMkernel adapters for 100Gbps NICs
5. Add the software NVMe over TCP adapter
6. Add NVMe/TCP target controllers for multipath connectivity

## Prerequisites

- Ansible 2.14+
- Python 3.9+
- Hitachi Vantara VSP One Block Ansible Collection: `hitachivantara.vspone_block`
- VMware Community Collection: `community.vmware`
- Network connectivity between the ESXi host and VSP One Block 28 storage ports
- ESXi 7.0 U3+ or 8.0+ with NVMe/TCP support

### Install Ansible Collections

```bash
ansible-galaxy collection install hitachivantara.vspone_block
ansible-galaxy collection install community.vmware
```

## Directory Structure

```
├── README.md
├── site.yml                          # Master playbook - runs all roles in sequence
├── inventory/
│   └── hosts.yml                     # Inventory file
├── ansible_vault_vars/
│   ├── ansible_vault_storage_var.yml # Storage credentials (encrypt with vault)
│   └── ansible_vault_esxi_var.yml    # ESXi credentials (encrypt with vault)
├── playbooks/
│   ├── 01_create_ldevs.yml           # Create LDEVs on VSP One Block 28
│   ├── 02_create_nvm_subsystem.yml   # Create NVM Subsystem with ports & host NQN
│   ├── 03_add_namespaces_and_paths.yml # Map LDEVs as namespaces with paths
│   ├── 04_configure_esxi_networking.yml # vSwitches + VMkernel adapters
│   ├── 05_add_nvme_tcp_adapter.yml   # Software NVMe/TCP adapter on ESXi
│   ├── 06_add_nvme_tcp_controllers.yml # NVMe/TCP target controllers
│   └── vars/
│       ├── storage_vars.yml          # Storage-side variables
│       └── esxi_vars.yml            # ESXi-side variables
└── roles/
    ├── vsp_create_ldevs/             # Role: Create LDEVs
    ├── vsp_create_nvm_subsystem/     # Role: Create NVM Subsystem
    ├── vsp_add_namespaces_and_paths/ # Role: Add namespaces & paths
    ├── esxi_configure_networking/    # Role: vSwitches & VMkernel adapters
    ├── esxi_add_nvme_tcp_adapter/    # Role: NVMe/TCP software adapter
    └── esxi_add_nvme_tcp_controllers/ # Role: NVMe/TCP target controllers
```

## Configuration

### 1. Encrypt Vault Files

Encrypt the credential files before use:

```bash
ansible-vault encrypt ansible_vault_vars/ansible_vault_storage_var.yml
ansible-vault encrypt ansible_vault_vars/ansible_vault_esxi_var.yml
```

### 2. Update Storage Variables

Edit `playbooks/vars/storage_vars.yml`:

| Variable | Description | Default |
|----------|-------------|---------|
| `pool_id` | Storage pool for LDEV creation | `0` |
| `ldev_start_id` | Starting LDEV ID | `0` |
| `ldev_count` | Number of LDEVs to create | `10` |
| `ldev_size` | Size of each LDEV | `10GB` |
| `nvm_subsystem_name` | NVM Subsystem name | `NVMeTCP_VSPOneB28` |
| `nvm_subsystem_host_mode` | Host mode for VMware | `VMWARE_EX` |
| `storage_ports` | NVMe/TCP storage ports | `["CL3-A", "CL4-A"]` |
| `host_nqn` | ESXi host NQN (get via `esxcli nvme info get`) | — |

### 3. Update ESXi Variables

Edit `playbooks/vars/esxi_vars.yml`:

| Variable | Description | Default |
|----------|-------------|---------|
| `vmnic_100g_1` / `vmnic_100g_2` | 100Gbps NIC names | `vmnic4` / `vmnic5` |
| `vswitch1_name` / `vswitch2_name` | vSwitch names | `vSwitch_NVMe_TCP_1` / `vSwitch_NVMe_TCP_2` |
| `vswitch_mtu` | MTU (jumbo frames) | `9000` |
| `vmk1_ip` / `vmk2_ip` | VMkernel adapter IPs | `192.168.10.15` / `192.168.11.15` |
| `storage_port1_ip` / `storage_port2_ip` | Storage port target IPs | `192.168.10.10` / `192.168.11.10` |
| `nvme_tcp_port` | NVMe/TCP port | `4420` |
| `subsystem_nqn` | Subsystem NQN (from storage after step 2) | — |

### 4. Update Vault Credentials

Edit `ansible_vault_vars/ansible_vault_storage_var.yml`:
- `storage_address` — REST API IP/FQDN of the VSP One Block 28
- `vault_storage_username` / `vault_storage_secret` — Storage credentials

Edit `ansible_vault_vars/ansible_vault_esxi_var.yml`:
- `esxi_hostname` — ESXi host FQDN or IP
- `vault_esxi_username` / `vault_esxi_password` — ESXi credentials

## Usage

### Run Everything End-to-End

```bash
ansible-playbook -i inventory/hosts.yml site.yml --ask-vault-pass
```

### Run Individual Playbooks

Run playbooks one at a time for step-by-step execution:

```bash
# Phase 1: Storage
ansible-playbook -i inventory/hosts.yml playbooks/01_create_ldevs.yml --ask-vault-pass
ansible-playbook -i inventory/hosts.yml playbooks/02_create_nvm_subsystem.yml --ask-vault-pass
ansible-playbook -i inventory/hosts.yml playbooks/03_add_namespaces_and_paths.yml --ask-vault-pass

# Phase 2: ESXi
ansible-playbook -i inventory/hosts.yml playbooks/04_configure_esxi_networking.yml --ask-vault-pass
ansible-playbook -i inventory/hosts.yml playbooks/05_add_nvme_tcp_adapter.yml --ask-vault-pass
ansible-playbook -i inventory/hosts.yml playbooks/06_add_nvme_tcp_controllers.yml --ask-vault-pass
```

## Network Topology

```
ESXi Host                                VSP One Block 28
┌─────────────────────┐                  ┌──────────────────────┐
│  vmnic4 (100G)      │──── Subnet 1 ───│  CL3-A (192.168.10.10)│
│   └─ vSwitch1       │  192.168.10.0/24 │                      │
│      └─ vmk1        │                  │                      │
│         192.168.10.15│                  │  NVM Subsystem       │
│                     │                  │   └─ Namespaces      │
│  vmnic5 (100G)      │──── Subnet 2 ───│  CL4-A (192.168.11.10)│
│   └─ vSwitch2       │  192.168.11.0/24 │                      │
│      └─ vmk2        │                  │                      │
│         192.168.11.15│                  │                      │
└─────────────────────┘                  └──────────────────────┘
         MTU 9000                                MTU 9000
```

## Playbook Details

### Playbook 1 — Create LDEVs

Uses `hitachivantara.vspone_block.vsp.hv_ldev` to create LDEVs in a loop. Each LDEV is assigned a sequential ID and named with the pattern `nvme_tcp_ldev_XXXX`.

### Playbook 2 — Create NVM Subsystem

Uses `hitachivantara.vspone_block.vsp.hv_nvm_subsystems` to create a subsystem with:
- Two NVMe/TCP storage ports
- Host mode set to `VMWARE_EX`
- Namespace security enabled
- ESXi host NQN registered

### Playbook 3 — Add Namespaces and Paths

Adds each LDEV as a namespace to the NVM Subsystem using `state: add_namespace`, mapping the host NQN as the access path for each namespace.

### Playbook 4 — Configure ESXi Networking

Creates a dedicated vSwitch per 100Gbps NIC (port binding), configures VMkernel adapters with static IPs on separate subnets, and tags them for NVMe/TCP traffic using `esxcli network ip interface tag add`.

### Playbook 5 — Add NVMe/TCP Adapter

Enables the software NVMe over TCP adapter on the ESXi host via `esxcli nvme fabrics enable` and verifies the adapter is listed.

### Playbook 6 — Add NVMe/TCP Target Controllers

Connects to the storage subsystem through two target controllers (one per storage port) using `esxcli nvme fabrics connect` for active-active multipath, then verifies visibility of namespaces.
