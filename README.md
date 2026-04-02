# NVMe/TCP End-to-End Automation: VSP One Block 28

Ansible automation for configuring NVMe over TCP connectivity between a Hitachi Vantara VSP One Block 28 storage system and compute hosts with 100Gbps network adapters.

## Host-Specific Guides

| Host OS | README | Master Playbook | Role |
|---------|--------|-----------------|------|
| **VMware ESXi** | [README.ESX.md](README.ESX.md) | `site.yml` | `nvme_tcp_end_to_end` |
| **Red Hat Enterprise Linux** | [README.RHEL.md](README.RHEL.md) | `site_rhel.yml` | `nvme_tcp_end_to_end_rhel` |

## Best Practices

See [BEST_PRACTICES.md](BEST_PRACTICES.md) for NVMe/TCP design guidelines covering subsystem-to-host ratios, port-to-namespace sizing, multipathing, network configuration, performance tuning, and troubleshooting.

## Common Prerequisites

- Ansible 2.14+
- Python 3.9+
- Hitachi Vantara VSP One Block Ansible Collection: `hitachivantara.vspone_block`
- Network connectivity between compute hosts and VSP One Block 28 storage ports

```bash
ansible-galaxy collection install hitachivantara.vspone_block
```

## Quick Start

### ESXi

```bash
ansible-playbook site.yml --ask-vault-pass
```

See [README.ESX.md](README.ESX.md) for full configuration details, variable reference, and network topology.

### RHEL

```bash
ansible-playbook site_rhel.yml --ask-vault-pass
```

See [README.RHEL.md](README.RHEL.md) for full configuration details, variable reference, and network topology.

## Key Differences

| Aspect | ESXi | RHEL |
|--------|------|------|
| Host mode | `VMWARE_EX` | `LINUX/IRIX` |
| Multipathing | VMware NVMe/TCP native (via vSphere) | NVMe native multipath (`nvme_core.multipath=Y`) |
| NIC setup | vSwitches + portgroups + VMkernel adapters | `nmcli` static IP configuration |
| NVMe adapter | `esxcli nvme fabrics enable` | `modprobe nvme_tcp` |
| Target connect | `esxcli nvme fabrics connect` | `nvme connect-all` via discovery.conf |
| IO policy | N/A (vSphere managed) | Round-robin via udev rule |
| Autoconnect | N/A | `nvmf-autoconnect` systemd service |
| Variable prefix | (none) | `rhel_` |

## Project Structure

```
├── README.md                          # This file
├── README.ESX.md                      # ESXi setup guide
├── README.RHEL.md                     # RHEL setup guide
├── site.yml                           # ESXi master playbook
├── site_rhel.yml                      # RHEL master playbook
├── inventory/
│   └── hosts.yml
├── ansible_vault_vars/
│   ├── ansible_vault_storage_var.yml  # Storage credentials
│   ├── ansible_vault_esxi_var.yml     # ESXi credentials
│   └── ansible_vault_rhel_var.yml     # RHEL credentials
├── playbooks/
│   ├── 01–06 individual playbooks     # ESXi step-by-step playbooks
│   └── vars/
│       ├── storage_vars.yml           # ESXi storage variables
│       ├── storage_rhel_vars.yml      # RHEL storage variables (rhel_ prefixed)
│       ├── esxi_vars.yml              # ESXi host variables
│       ├── rhel_vars.yml              # RHEL host variables
│       ├── generated_nvm_nqn.yml      # Auto-generated NQN (ESXi)
│       └── generated_rhel_nvm_nqn.yml # Auto-generated NQN (RHEL)
├── roles/
│   ├── nvme_tcp_end_to_end/           # ESXi combined role (all 6 steps)
│   ├── nvme_tcp_end_to_end_rhel/      # RHEL combined role (all 6 steps)
│   ├── vsp_create_ldevs/              # ESXi individual roles
│   ├── vsp_create_nvm_subsystem/
│   ├── vsp_add_namespaces_and_paths/
│   ├── esxi_configure_networking/
│   ├── esxi_add_nvme_tcp_adapter/
│   └── esxi_add_nvme_tcp_controllers/
└── examples/
    ├── nvm_subsystem_facts.yml
    └── nvm_subsystems.yml
```
