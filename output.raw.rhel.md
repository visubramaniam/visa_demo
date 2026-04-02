# Ansible Playbook Output: NVMe/TCP End-to-End Setup

visubramaniam@MQ7HY4M9M0 visa_demo % ansible-playbook site_rhel.yml
[WARNING]: No inventory was parsed, only implicit localhost is available
[WARNING]: provided hosts list is empty, only localhost is available. Note that the implicit localhost does not match 'all'

PLAY [NVMe/TCP End-to-End Setup: VSP One Block 28 + RHEL] ****************************************************************************

TASK [roles/nvme_tcp_end_to_end_rhel : Step 1 - Create LDEVs for NVMe/TCP namespaces] ************************************************
Thursday 02 April 2026  00:30:14 -0400 (0:00:00.030)       0:00:00.030 ******** 
Thursday 02 April 2026  00:30:14 -0400 (0:00:00.029)       0:00:00.029 ******** 
ok: [localhost] => (item=0)
ok: [localhost] => (item=1)
ok: [localhost] => (item=2)
ok: [localhost] => (item=3)
ok: [localhost] => (item=4)
ok: [localhost] => (item=5)
ok: [localhost] => (item=6)
ok: [localhost] => (item=7)
ok: [localhost] => (item=8)
ok: [localhost] => (item=9)

TASK [roles/nvme_tcp_end_to_end_rhel : Step 1 - Display created LDEV details] ********************************************************
Thursday 02 April 2026  00:32:21 -0400 (0:02:06.852)       0:02:06.882 ******** 
Thursday 02 April 2026  00:32:21 -0400 (0:02:06.852)       0:02:06.881 ******** 
ok: [localhost] => (item=0) => {
    "msg": "LDEV 6144 created successfully"
}
ok: [localhost] => (item=1) => {
    "msg": "LDEV 6145 created successfully"
}
ok: [localhost] => (item=2) => {
    "msg": "LDEV 6146 created successfully"
}
ok: [localhost] => (item=3) => {
    "msg": "LDEV 6147 created successfully"
}
ok: [localhost] => (item=4) => {
    "msg": "LDEV 6148 created successfully"
}
ok: [localhost] => (item=5) => {
    "msg": "LDEV 6149 created successfully"
}
ok: [localhost] => (item=6) => {
    "msg": "LDEV 6150 created successfully"
}
ok: [localhost] => (item=7) => {
    "msg": "LDEV 6151 created successfully"
}
ok: [localhost] => (item=8) => {
    "msg": "LDEV 6152 created successfully"
}
ok: [localhost] => (item=9) => {
    "msg": "LDEV 6153 created successfully"
}

TASK [roles/nvme_tcp_end_to_end_rhel : Step 2 - Verify nvme-cli is installed] ********************************************************
Thursday 02 April 2026  00:32:21 -0400 (0:00:00.146)       0:02:07.029 ******** 
Thursday 02 April 2026  00:32:21 -0400 (0:00:00.146)       0:02:07.027 ******** 
[WARNING]: Host 'localhost' is using the discovered Python interpreter at '/usr/bin/python3.12', but future installation of another Python interpreter could cause a different interpreter to be discovered. See <https://docs.ansible.com/ansible-core/2.20/reference_appendices/interpreter_discovery.html> for more information.
ok: [localhost -> 192.168.53.160]

TASK [roles/nvme_tcp_end_to_end_rhel : Step 2 - Install nvme-cli if not present] *****************************************************
Thursday 02 April 2026  00:32:24 -0400 (0:00:02.999)       0:02:10.028 ******** 
Thursday 02 April 2026  00:32:24 -0400 (0:00:02.999)       0:02:10.027 ******** 
skipping: [localhost]

TASK [roles/nvme_tcp_end_to_end_rhel : Step 2 - Display installed nvme-cli package] **************************************************
Thursday 02 April 2026  00:32:24 -0400 (0:00:00.022)       0:02:10.051 ******** 
Thursday 02 April 2026  00:32:24 -0400 (0:00:00.022)       0:02:10.050 ******** 
ok: [localhost] => {
    "msg": "nvme-cli: ['nvme-cli-1.16-9.el8.x86_64']"
}

TASK [roles/nvme_tcp_end_to_end_rhel : Step 2 - Read host NQN from RHEL host] ********************************************************
Thursday 02 April 2026  00:32:24 -0400 (0:00:00.030)       0:02:10.082 ******** 
Thursday 02 April 2026  00:32:24 -0400 (0:00:00.030)       0:02:10.081 ******** 
ok: [localhost -> 192.168.53.160]

TASK [roles/nvme_tcp_end_to_end_rhel : Step 2 - Set host NQN fact for use in Steps 3 and 4] ******************************************
Thursday 02 April 2026  00:32:25 -0400 (0:00:01.094)       0:02:11.177 ******** 
Thursday 02 April 2026  00:32:25 -0400 (0:00:01.094)       0:02:11.175 ******** 
ok: [localhost]

TASK [roles/nvme_tcp_end_to_end_rhel : Step 2 - Display RHEL host NQN] ***************************************************************
Thursday 02 April 2026  00:32:25 -0400 (0:00:00.043)       0:02:11.221 ******** 
Thursday 02 April 2026  00:32:25 -0400 (0:00:00.043)       0:02:11.219 ******** 
ok: [localhost] => {
    "msg": "RHEL Host NQN: nqn.2014-08.org.nvmexpress:uuid:ca845a3c-fe2f-4e6a-96dd-99b094774113"
}

TASK [roles/nvme_tcp_end_to_end_rhel : Step 2 - Configure static IP on NIC interface 1 (ens97f1)] ************************************
Thursday 02 April 2026  00:32:25 -0400 (0:00:00.016)       0:02:11.237 ******** 
Thursday 02 April 2026  00:32:25 -0400 (0:00:00.016)       0:02:11.236 ******** 
changed: [localhost -> 192.168.53.160]

TASK [roles/nvme_tcp_end_to_end_rhel : Step 2 - Configure static IP on NIC interface 2 (ens99f1)] ************************************
Thursday 02 April 2026  00:32:27 -0400 (0:00:01.134)       0:02:12.372 ******** 
Thursday 02 April 2026  00:32:27 -0400 (0:00:01.134)       0:02:12.371 ******** 
changed: [localhost -> 192.168.53.160]

TASK [roles/nvme_tcp_end_to_end_rhel : Step 2 - Verify NIC interface IP addresses] ***************************************************
Thursday 02 April 2026  00:32:28 -0400 (0:00:01.110)       0:02:13.482 ******** 
Thursday 02 April 2026  00:32:28 -0400 (0:00:01.110)       0:02:13.481 ******** 
ok: [localhost -> 192.168.53.160]

TASK [roles/nvme_tcp_end_to_end_rhel : Step 2 - Display NIC IP addresses] ************************************************************
Thursday 02 April 2026  00:32:29 -0400 (0:00:01.094)       0:02:14.577 ******** 
Thursday 02 April 2026  00:32:29 -0400 (0:00:01.094)       0:02:14.575 ******** 
ok: [localhost] => {
    "ip_addr_output.stdout_lines": [
        "1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000",
        "    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00",
        "    inet 127.0.0.1/8 scope host lo",
        "       valid_lft forever preferred_lft forever",
        "    inet6 ::1/128 scope host ",
        "       valid_lft forever preferred_lft forever",
        "2: ens8f0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc mq state UP group default qlen 1000",
        "    link/ether f0:b2:b9:16:a4:78 brd ff:ff:ff:ff:ff:ff",
        "    altname enp23s0f0",
        "    inet 192.168.53.160/22 brd 192.168.55.255 scope global noprefixroute ens8f0",
        "       valid_lft forever preferred_lft forever",
        "    inet6 fd01:52::f2b2:b9ff:fe16:a478/64 scope global dynamic noprefixroute ",
        "       valid_lft 2591968sec preferred_lft 604768sec",
        "    inet6 fe80::f2b2:b9ff:fe16:a478/64 scope link noprefixroute ",
        "       valid_lft forever preferred_lft forever",
        "3: ens8f1: <NO-CARRIER,BROADCAST,MULTICAST,UP> mtu 1500 qdisc mq state DOWN group default qlen 1000",
        "    link/ether f0:b2:b9:16:a4:79 brd ff:ff:ff:ff:ff:ff",
        "    altname enp23s0f1",
        "4: ens8f2: <NO-CARRIER,BROADCAST,MULTICAST,UP> mtu 1500 qdisc mq state DOWN group default qlen 1000",
        "    link/ether f0:b2:b9:16:a4:7a brd ff:ff:ff:ff:ff:ff",
        "    altname enp23s0f2",
        "5: ens8f3: <NO-CARRIER,BROADCAST,MULTICAST,UP> mtu 1500 qdisc mq state DOWN group default qlen 1000",
        "    link/ether f0:b2:b9:16:a4:7b brd ff:ff:ff:ff:ff:ff",
        "    altname enp23s0f3",
        "6: ens97f0: <NO-CARRIER,BROADCAST,MULTICAST,UP> mtu 1500 qdisc mq state DOWN group default qlen 1000",
        "    link/ether 58:a2:e1:11:f5:5c brd ff:ff:ff:ff:ff:ff",
        "    altname enp75s0f0",
        "7: ens97f1: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc mq state UP group default qlen 1000",
        "    link/ether 58:a2:e1:11:f5:5d brd ff:ff:ff:ff:ff:ff",
        "    altname enp75s0f1",
        "    inet 192.168.10.45/24 brd 192.168.10.255 scope global noprefixroute ens97f1",
        "       valid_lft forever preferred_lft forever",
        "    inet6 fe80::d4e9:6b96:406a:bb54/64 scope link noprefixroute ",
        "       valid_lft forever preferred_lft forever",
        "8: ens45f0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc mq state UP group default qlen 1000",
        "    link/ether 9c:63:c0:95:17:56 brd ff:ff:ff:ff:ff:ff",
        "    altname enp101s0f0",
        "    inet 172.28.53.160/16 brd 172.28.255.255 scope global noprefixroute ens45f0",
        "       valid_lft forever preferred_lft forever",
        "    inet6 fd01:52::9e63:c0ff:fe95:1756/64 scope global dynamic mngtmpaddr ",
        "       valid_lft 2591967sec preferred_lft 604767sec",
        "    inet6 fe80::9e63:c0ff:fe95:1756/64 scope link ",
        "       valid_lft forever preferred_lft forever",
        "9: ens45f1: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc mq state UP group default qlen 1000",
        "    link/ether 9c:63:c0:95:17:57 brd ff:ff:ff:ff:ff:ff",
        "    altname enp101s0f1",
        "    inet 172.29.53.160/16 brd 172.29.255.255 scope global noprefixroute ens45f1",
        "       valid_lft forever preferred_lft forever",
        "    inet6 fd01:52::9e63:c0ff:fe95:1757/64 scope global dynamic mngtmpaddr ",
        "       valid_lft 2591967sec preferred_lft 604767sec",
        "    inet6 fe80::9e63:c0ff:fe95:1757/64 scope link ",
        "       valid_lft forever preferred_lft forever",
        "10: ens99f0: <NO-CARRIER,BROADCAST,MULTICAST,UP> mtu 1500 qdisc mq state DOWN group default qlen 1000",
        "    link/ether 58:a2:e1:12:0c:6c brd ff:ff:ff:ff:ff:ff",
        "    altname enp202s0f0",
        "11: ens99f1: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc mq state UP group default qlen 1000",
        "    link/ether 58:a2:e1:12:0c:6d brd ff:ff:ff:ff:ff:ff",
        "    altname enp202s0f1",
        "    inet 192.168.20.45/24 brd 192.168.20.255 scope global noprefixroute ens99f1",
        "       valid_lft forever preferred_lft forever",
        "    inet6 fe80::9f1:6708:aa89:c2ed/64 scope link tentative noprefixroute ",
        "       valid_lft forever preferred_lft forever",
        "12: usb0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UNKNOWN group default qlen 1000",
        "    link/ether ea:22:27:f4:67:70 brd ff:ff:ff:ff:ff:ff"
    ]
}

TASK [roles/nvme_tcp_end_to_end_rhel : Step 2 - Verify connectivity to storage port 1] ***********************************************
Thursday 02 April 2026  00:32:29 -0400 (0:00:00.028)       0:02:14.605 ******** 
Thursday 02 April 2026  00:32:29 -0400 (0:00:00.028)       0:02:14.603 ******** 
ok: [localhost -> 192.168.53.160]

TASK [roles/nvme_tcp_end_to_end_rhel : Step 2 - Verify connectivity to storage port 2] ***********************************************
Thursday 02 April 2026  00:32:33 -0400 (0:00:04.160)       0:02:18.765 ******** 
Thursday 02 April 2026  00:32:33 -0400 (0:00:04.160)       0:02:18.764 ******** 
ok: [localhost -> 192.168.53.160]

TASK [roles/nvme_tcp_end_to_end_rhel : Step 2 - Display connectivity results] ********************************************************
Thursday 02 April 2026  00:32:37 -0400 (0:00:04.140)       0:02:22.906 ******** 
Thursday 02 April 2026  00:32:37 -0400 (0:00:04.140)       0:02:22.904 ******** 
ok: [localhost] => {
    "msg": [
        "Ping to 192.168.10.30: SUCCESS",
        "Ping to 192.168.20.30: SUCCESS"
    ]
}

TASK [roles/nvme_tcp_end_to_end_rhel : Step 3 - Create NVM Subsystem with ports and host NQN] ****************************************
Thursday 02 April 2026  00:32:37 -0400 (0:00:00.017)       0:02:22.923 ******** 
Thursday 02 April 2026  00:32:37 -0400 (0:00:00.017)       0:02:22.922 ******** 
changed: [localhost]

TASK [roles/nvme_tcp_end_to_end_rhel : Step 3 - Display NVM Subsystem creation result] ***********************************************
Thursday 02 April 2026  00:33:06 -0400 (0:00:28.725)       0:02:51.648 ******** 
Thursday 02 April 2026  00:33:06 -0400 (0:00:28.725)       0:02:51.647 ******** 
ok: [localhost] => {
    "nvm_subsystem_result": {
        "changed": true,
        "failed": false,
        "nvm_subsystems": [
            {
                "host_nqn_info": [
                    {
                        "host_nqn": "nqn.2014-08.org.nvmexpress:uuid:ca845a3c-fe2f-4e6a-96dd-99b094774113",
                        "host_nqn_nickname": "rhel_host_nqn"
                    }
                ],
                "namespace_paths_info": [
                    {
                        "host_nqn": "nqn.2014-08.org.nvmexpress:uuid:ca845a3c-fe2f-4e6a-96dd-99b094774113",
                        "ldev_id": 6144,
                        "ldev_id_hex": "00:18:00",
                        "namespace_id": 1
                    },
                    {
                        "host_nqn": "nqn.2014-08.org.nvmexpress:uuid:ca845a3c-fe2f-4e6a-96dd-99b094774113",
                        "ldev_id": 6145,
                        "ldev_id_hex": "00:18:01",
                        "namespace_id": 2
                    },
                    {
                        "host_nqn": "nqn.2014-08.org.nvmexpress:uuid:ca845a3c-fe2f-4e6a-96dd-99b094774113",
                        "ldev_id": 6146,
                        "ldev_id_hex": "00:18:02",
                        "namespace_id": 3
                    },
                    {
                        "host_nqn": "nqn.2014-08.org.nvmexpress:uuid:ca845a3c-fe2f-4e6a-96dd-99b094774113",
                        "ldev_id": 6147,
                        "ldev_id_hex": "00:18:03",
                        "namespace_id": 4
                    },
                    {
                        "host_nqn": "nqn.2014-08.org.nvmexpress:uuid:ca845a3c-fe2f-4e6a-96dd-99b094774113",
                        "ldev_id": 6148,
                        "ldev_id_hex": "00:18:04",
                        "namespace_id": 5
                    },
                    {
                        "host_nqn": "nqn.2014-08.org.nvmexpress:uuid:ca845a3c-fe2f-4e6a-96dd-99b094774113",
                        "ldev_id": 6149,
                        "ldev_id_hex": "00:18:05",
                        "namespace_id": 6
                    },
                    {
                        "host_nqn": "nqn.2014-08.org.nvmexpress:uuid:ca845a3c-fe2f-4e6a-96dd-99b094774113",
                        "ldev_id": 6150,
                        "ldev_id_hex": "00:18:06",
                        "namespace_id": 7
                    },
                    {
                        "host_nqn": "nqn.2014-08.org.nvmexpress:uuid:ca845a3c-fe2f-4e6a-96dd-99b094774113",
                        "ldev_id": 6151,
                        "ldev_id_hex": "00:18:07",
                        "namespace_id": 8
                    },
                    {
                        "host_nqn": "nqn.2014-08.org.nvmexpress:uuid:ca845a3c-fe2f-4e6a-96dd-99b094774113",
                        "ldev_id": 6152,
                        "ldev_id_hex": "00:18:08",
                        "namespace_id": 9
                    },
                    {
                        "host_nqn": "nqn.2014-08.org.nvmexpress:uuid:ca845a3c-fe2f-4e6a-96dd-99b094774113",
                        "ldev_id": 6153,
                        "ldev_id_hex": "00:18:09",
                        "namespace_id": 10
                    }
                ],
                "namespaces_info": [
                    {
                        "block_capacity": 20971520,
                        "capacity_in_mb": 10240.0,
                        "capacity_in_unit": "10.00GB",
                        "ldev_id": 6144,
                        "ldev_id_hex": "00:18:00",
                        "namespace_id": 1,
                        "namespace_nickname": "rhel_nvme_tcp_ldev_ns_6144"
                    },
                    {
                        "block_capacity": 20971520,
                        "capacity_in_mb": 10240.0,
                        "capacity_in_unit": "10.00GB",
                        "ldev_id": 6145,
                        "ldev_id_hex": "00:18:01",
                        "namespace_id": 2,
                        "namespace_nickname": "rhel_nvme_tcp_ldev_ns_6145"
                    },
                    {
                        "block_capacity": 20971520,
                        "capacity_in_mb": 10240.0,
                        "capacity_in_unit": "10.00GB",
                        "ldev_id": 6146,
                        "ldev_id_hex": "00:18:02",
                        "namespace_id": 3,
                        "namespace_nickname": "rhel_nvme_tcp_ldev_ns_6146"
                    },
                    {
                        "block_capacity": 20971520,
                        "capacity_in_mb": 10240.0,
                        "capacity_in_unit": "10.00GB",
                        "ldev_id": 6147,
                        "ldev_id_hex": "00:18:03",
                        "namespace_id": 4,
                        "namespace_nickname": "rhel_nvme_tcp_ldev_ns_6147"
                    },
                    {
                        "block_capacity": 20971520,
                        "capacity_in_mb": 10240.0,
                        "capacity_in_unit": "10.00GB",
                        "ldev_id": 6148,
                        "ldev_id_hex": "00:18:04",
                        "namespace_id": 5,
                        "namespace_nickname": "rhel_nvme_tcp_ldev_ns_6148"
                    },
                    {
                        "block_capacity": 20971520,
                        "capacity_in_mb": 10240.0,
                        "capacity_in_unit": "10.00GB",
                        "ldev_id": 6149,
                        "ldev_id_hex": "00:18:05",
                        "namespace_id": 6,
                        "namespace_nickname": "rhel_nvme_tcp_ldev_ns_6149"
                    },
                    {
                        "block_capacity": 20971520,
                        "capacity_in_mb": 10240.0,
                        "capacity_in_unit": "10.00GB",
                        "ldev_id": 6150,
                        "ldev_id_hex": "00:18:06",
                        "namespace_id": 7,
                        "namespace_nickname": "rhel_nvme_tcp_ldev_ns_6150"
                    },
                    {
                        "block_capacity": 20971520,
                        "capacity_in_mb": 10240.0,
                        "capacity_in_unit": "10.00GB",
                        "ldev_id": 6151,
                        "ldev_id_hex": "00:18:07",
                        "namespace_id": 8,
                        "namespace_nickname": "rhel_nvme_tcp_ldev_ns_6151"
                    },
                    {
                        "block_capacity": 20971520,
                        "capacity_in_mb": 10240.0,
                        "capacity_in_unit": "10.00GB",
                        "ldev_id": 6152,
                        "ldev_id_hex": "00:18:08",
                        "namespace_id": 9,
                        "namespace_nickname": "rhel_nvme_tcp_ldev_ns_6152"
                    },
                    {
                        "block_capacity": 20971520,
                        "capacity_in_mb": 10240.0,
                        "capacity_in_unit": "10.00GB",
                        "ldev_id": 6153,
                        "ldev_id_hex": "00:18:09",
                        "namespace_id": 10,
                        "namespace_nickname": "rhel_nvme_tcp_ldev_ns_6153"
                    }
                ],
                "nvm_subsystem_info": {
                    "host_mode": "LINUX/IRIX",
                    "namespace_security_setting": "Enable",
                    "nvm_subsystem_id": 1,
                    "nvm_subsystem_name": "NVMeTCP_RHEL_VSPOneB28",
                    "resource_group_id": 0,
                    "t10pi_mode": "Disable"
                },
                "port_info": [
                    {
                        "port_id": "CL3-D",
                        "port_type": "NVME_TCP"
                    },
                    {
                        "port_id": "CL4-D",
                        "port_type": "NVME_TCP"
                    }
                ],
                "storage_serial_number": "840498"
            }
        ],
        "user_consent_required": "Hitachi Vantara LLC collects usage data such as storage model, storage serial number, operation name, status (success or failure),and duration. This data is collected for product improvement purposes only. It remains confidential and it is not shared with any third parties. To provide your consent, run the accept_user_consent.yml playbook."
    }
}

TASK [roles/nvme_tcp_end_to_end_rhel : Step 3 - Set storage serial and subsystem ID from creation result] ****************************
Thursday 02 April 2026  00:33:06 -0400 (0:00:00.020)       0:02:51.669 ******** 
Thursday 02 April 2026  00:33:06 -0400 (0:00:00.020)       0:02:51.668 ******** 
ok: [localhost]

TASK [roles/nvme_tcp_end_to_end_rhel : Step 3 - Construct subsystem NQN] *************************************************************
Thursday 02 April 2026  00:33:06 -0400 (0:00:00.038)       0:02:51.707 ******** 
Thursday 02 April 2026  00:33:06 -0400 (0:00:00.038)       0:02:51.706 ******** 
ok: [localhost]

TASK [roles/nvme_tcp_end_to_end_rhel : Step 3 - Save subsystem NQN to generated vars file] *******************************************
Thursday 02 April 2026  00:33:06 -0400 (0:00:00.023)       0:02:51.730 ******** 
Thursday 02 April 2026  00:33:06 -0400 (0:00:00.023)       0:02:51.729 ******** 
ok: [localhost]

TASK [roles/nvme_tcp_end_to_end_rhel : Step 3 - Display constructed subsystem NQN] ***************************************************
Thursday 02 April 2026  00:33:07 -0400 (0:00:00.818)       0:02:52.549 ******** 
Thursday 02 April 2026  00:33:07 -0400 (0:00:00.818)       0:02:52.547 ******** 
ok: [localhost] => {
    "msg": "Subsystem NQN saved: nqn.1994-04.jp.co.hitachi:nvme:storage-subsystem-sn.8-40498-nvmssid.00001"
}

TASK [roles/nvme_tcp_end_to_end_rhel : Step 4 - Add namespaces and namespace paths to NVM Subsystem] *********************************
Thursday 02 April 2026  00:33:07 -0400 (0:00:00.017)       0:02:52.567 ******** 
Thursday 02 April 2026  00:33:07 -0400 (0:00:00.017)       0:02:52.565 ******** 
changed: [localhost] => (item=0)
changed: [localhost] => (item=1)
changed: [localhost] => (item=2)
changed: [localhost] => (item=3)
changed: [localhost] => (item=4)
changed: [localhost] => (item=5)
changed: [localhost] => (item=6)
changed: [localhost] => (item=7)
changed: [localhost] => (item=8)
changed: [localhost] => (item=9)

TASK [roles/nvme_tcp_end_to_end_rhel : Step 4 - Display namespace creation results] **************************************************
Thursday 02 April 2026  00:35:05 -0400 (0:01:57.913)       0:04:50.480 ******** 
Thursday 02 April 2026  00:35:05 -0400 (0:01:57.913)       0:04:50.479 ******** 
ok: [localhost] => (item=0) => {
    "msg": "Namespace for LDEV 6144 added successfully"
}
ok: [localhost] => (item=1) => {
    "msg": "Namespace for LDEV 6145 added successfully"
}
ok: [localhost] => (item=2) => {
    "msg": "Namespace for LDEV 6146 added successfully"
}
ok: [localhost] => (item=3) => {
    "msg": "Namespace for LDEV 6147 added successfully"
}
ok: [localhost] => (item=4) => {
    "msg": "Namespace for LDEV 6148 added successfully"
}
ok: [localhost] => (item=5) => {
    "msg": "Namespace for LDEV 6149 added successfully"
}
ok: [localhost] => (item=6) => {
    "msg": "Namespace for LDEV 6150 added successfully"
}
ok: [localhost] => (item=7) => {
    "msg": "Namespace for LDEV 6151 added successfully"
}
ok: [localhost] => (item=8) => {
    "msg": "Namespace for LDEV 6152 added successfully"
}
ok: [localhost] => (item=9) => {
    "msg": "Namespace for LDEV 6153 added successfully"
}

TASK [roles/nvme_tcp_end_to_end_rhel : Step 5 - Load nvme_tcp kernel module] *********************************************************
Thursday 02 April 2026  00:35:05 -0400 (0:00:00.081)       0:04:50.562 ******** 
Thursday 02 April 2026  00:35:05 -0400 (0:00:00.081)       0:04:50.561 ******** 
changed: [localhost -> 192.168.53.160]

TASK [roles/nvme_tcp_end_to_end_rhel : Step 5 - Verify nvme_tcp module is loaded] ****************************************************
Thursday 02 April 2026  00:35:06 -0400 (0:00:01.571)       0:04:52.133 ******** 
Thursday 02 April 2026  00:35:06 -0400 (0:00:01.571)       0:04:52.132 ******** 
ok: [localhost -> 192.168.53.160]

TASK [roles/nvme_tcp_end_to_end_rhel : Step 5 - Display nvme_tcp module status] ******************************************************
Thursday 02 April 2026  00:35:07 -0400 (0:00:01.047)       0:04:53.181 ******** 
Thursday 02 April 2026  00:35:07 -0400 (0:00:01.047)       0:04:53.180 ******** 
ok: [localhost] => {
    "lsmod_result.stdout_lines": [
        "nvme_tcp               36864  0",
        "nvme_fabrics           24576  1 nvme_tcp",
        "nvme_core             139264  2 nvme_tcp,nvme_fabrics"
    ]
}

TASK [roles/nvme_tcp_end_to_end_rhel : Step 5 - Check if auto-generated NQN file exists] *********************************************
Thursday 02 April 2026  00:35:07 -0400 (0:00:00.028)       0:04:53.210 ******** 
Thursday 02 April 2026  00:35:07 -0400 (0:00:00.028)       0:04:53.208 ******** 
ok: [localhost]

TASK [roles/nvme_tcp_end_to_end_rhel : Step 5 - Load auto-generated subsystem NQN] ***************************************************
Thursday 02 April 2026  00:35:08 -0400 (0:00:00.479)       0:04:53.689 ******** 
Thursday 02 April 2026  00:35:08 -0400 (0:00:00.479)       0:04:53.687 ******** 
ok: [localhost]

TASK [roles/nvme_tcp_end_to_end_rhel : Step 5 - Display subsystem NQN being used] ****************************************************
Thursday 02 April 2026  00:35:08 -0400 (0:00:00.027)       0:04:53.716 ******** 
Thursday 02 April 2026  00:35:08 -0400 (0:00:00.027)       0:04:53.715 ******** 
ok: [localhost] => {
    "msg": "Using subsystem NQN: nqn.1994-04.jp.co.hitachi:nvme:storage-subsystem-sn.8-40498-nvmssid.00001"
}

TASK [roles/nvme_tcp_end_to_end_rhel : Step 5 - Discover NVMe targets via storage port 1] ********************************************
Thursday 02 April 2026  00:35:08 -0400 (0:00:00.024)       0:04:53.741 ******** 
Thursday 02 April 2026  00:35:08 -0400 (0:00:00.024)       0:04:53.739 ******** 
ok: [localhost -> 192.168.53.160]

TASK [roles/nvme_tcp_end_to_end_rhel : Step 5 - Display discovery results for storage port 1] ****************************************
Thursday 02 April 2026  00:35:09 -0400 (0:00:01.035)       0:04:54.776 ******** 
Thursday 02 April 2026  00:35:09 -0400 (0:00:01.035)       0:04:54.775 ******** 
ok: [localhost] => {
    "discover_port1.stdout_lines": [
        "",
        "Discovery Log Number of Records 1, Generation counter 2",
        "=====Discovery Log Entry 0======",
        "trtype:  tcp",
        "adrfam:  ipv4",
        "subtype: nvme subsystem",
        "treq:    not specified, sq flow control disable supported",
        "portid:  0",
        "trsvcid: 4420",
        "subnqn:  nqn.1994-04.jp.co.hitachi:nvme:storage-subsystem-sn.8-40498-nvmssid.00001",
        "traddr:  192.168.10.30",
        "sectype: none"
    ]
}

TASK [roles/nvme_tcp_end_to_end_rhel : Step 5 - Discover NVMe targets via storage port 2] ********************************************
Thursday 02 April 2026  00:35:09 -0400 (0:00:00.026)       0:04:54.803 ******** 
Thursday 02 April 2026  00:35:09 -0400 (0:00:00.026)       0:04:54.801 ******** 
ok: [localhost -> 192.168.53.160]

TASK [roles/nvme_tcp_end_to_end_rhel : Step 5 - Display discovery results for storage port 2] ****************************************
Thursday 02 April 2026  00:35:10 -0400 (0:00:01.049)       0:04:55.853 ******** 
Thursday 02 April 2026  00:35:10 -0400 (0:00:01.050)       0:04:55.851 ******** 
ok: [localhost] => {
    "discover_port2.stdout_lines": [
        "",
        "Discovery Log Number of Records 1, Generation counter 2",
        "=====Discovery Log Entry 0======",
        "trtype:  tcp",
        "adrfam:  ipv4",
        "subtype: nvme subsystem",
        "treq:    not specified, sq flow control disable supported",
        "portid:  1",
        "trsvcid: 4420",
        "subnqn:  nqn.1994-04.jp.co.hitachi:nvme:storage-subsystem-sn.8-40498-nvmssid.00001",
        "traddr:  192.168.20.30",
        "sectype: none"
    ]
}

TASK [roles/nvme_tcp_end_to_end_rhel : Step 5 - Configure /etc/nvme/discovery.conf] **************************************************
Thursday 02 April 2026  00:35:10 -0400 (0:00:00.024)       0:04:55.877 ******** 
Thursday 02 April 2026  00:35:10 -0400 (0:00:00.024)       0:04:55.876 ******** 
ok: [localhost -> 192.168.53.160]

TASK [roles/nvme_tcp_end_to_end_rhel : Step 5 - Disconnect any stale NVMe-oF sessions] ***********************************************
Thursday 02 April 2026  00:35:12 -0400 (0:00:01.727)       0:04:57.605 ******** 
Thursday 02 April 2026  00:35:12 -0400 (0:00:01.727)       0:04:57.603 ******** 
ok: [localhost -> 192.168.53.160]

TASK [roles/nvme_tcp_end_to_end_rhel : Step 5 - Connect to NVMe subsystem via storage port 1] ****************************************
Thursday 02 April 2026  00:35:14 -0400 (0:00:01.669)       0:04:59.274 ******** 
Thursday 02 April 2026  00:35:14 -0400 (0:00:01.669)       0:04:59.273 ******** 
changed: [localhost -> 192.168.53.160]

TASK [roles/nvme_tcp_end_to_end_rhel : Step 5 - Display connect port 1 result] *******************************************************
Thursday 02 April 2026  00:35:15 -0400 (0:00:01.125)       0:05:00.400 ******** 
Thursday 02 April 2026  00:35:15 -0400 (0:00:01.125)       0:05:00.398 ******** 
ok: [localhost] => {
    "connect_port1_result": {
        "changed": true,
        "cmd": [
            "nvme",
            "connect",
            "--transport=tcp",
            "--nqn=nqn.1994-04.jp.co.hitachi:nvme:storage-subsystem-sn.8-40498-nvmssid.00001",
            "--traddr=192.168.10.30",
            "--trsvcid=4420",
            "--host-traddr=192.168.10.45"
        ],
        "delta": "0:00:00.055519",
        "end": "2026-04-02 00:35:15.067387",
        "failed": false,
        "msg": "",
        "rc": 0,
        "start": "2026-04-02 00:35:15.011868",
        "stderr": "",
        "stderr_lines": [],
        "stdout": "",
        "stdout_lines": [],
        "warnings": [
            "Host 'localhost' is using the discovered Python interpreter at '/usr/bin/python3.12', but future installation of another Python interpreter could cause a different interpreter to be discovered."
        ]
    }
}

TASK [roles/nvme_tcp_end_to_end_rhel : Step 5 - Connect to NVMe subsystem via storage port 2] ****************************************
Thursday 02 April 2026  00:35:15 -0400 (0:00:00.018)       0:05:00.418 ******** 
Thursday 02 April 2026  00:35:15 -0400 (0:00:00.018)       0:05:00.417 ******** 
changed: [localhost -> 192.168.53.160]

TASK [roles/nvme_tcp_end_to_end_rhel : Step 5 - Display connect port 2 result] *******************************************************
Thursday 02 April 2026  00:35:16 -0400 (0:00:01.104)       0:05:01.522 ******** 
Thursday 02 April 2026  00:35:16 -0400 (0:00:01.104)       0:05:01.521 ******** 
ok: [localhost] => {
    "connect_port2_result": {
        "changed": true,
        "cmd": [
            "nvme",
            "connect",
            "--transport=tcp",
            "--nqn=nqn.1994-04.jp.co.hitachi:nvme:storage-subsystem-sn.8-40498-nvmssid.00001",
            "--traddr=192.168.20.30",
            "--trsvcid=4420",
            "--host-traddr=192.168.20.45"
        ],
        "delta": "0:00:00.049620",
        "end": "2026-04-02 00:35:16.199027",
        "failed": false,
        "msg": "",
        "rc": 0,
        "start": "2026-04-02 00:35:16.149407",
        "stderr": "",
        "stderr_lines": [],
        "stdout": "",
        "stdout_lines": [],
        "warnings": [
            "Host 'localhost' is using the discovered Python interpreter at '/usr/bin/python3.12', but future installation of another Python interpreter could cause a different interpreter to be discovered."
        ]
    }
}

TASK [roles/nvme_tcp_end_to_end_rhel : Step 5 - Enable and start nvmf-autoconnect service] *******************************************
Thursday 02 April 2026  00:35:16 -0400 (0:00:00.018)       0:05:01.541 ******** 
Thursday 02 April 2026  00:35:16 -0400 (0:00:00.018)       0:05:01.540 ******** 
changed: [localhost -> 192.168.53.160]

TASK [roles/nvme_tcp_end_to_end_rhel : Step 5 - List connected NVMe namespaces] ******************************************************
Thursday 02 April 2026  00:35:18 -0400 (0:00:01.703)       0:05:03.245 ******** 
Thursday 02 April 2026  00:35:18 -0400 (0:00:01.703)       0:05:03.243 ******** 
ok: [localhost -> 192.168.53.160]

TASK [roles/nvme_tcp_end_to_end_rhel : Step 5 - Display NVMe namespaces] *************************************************************
Thursday 02 April 2026  00:35:19 -0400 (0:00:01.238)       0:05:04.483 ******** 
Thursday 02 April 2026  00:35:19 -0400 (0:00:01.238)       0:05:04.482 ******** 
ok: [localhost] => {
    "nvme_list_result.stdout_lines": [
        "Node                  SN                   Model                                    Namespace Usage                      Format           FW Rev  ",
        "--------------------- -------------------- ---------------------------------------- --------- -------------------------- ---------------- --------",
        "/dev/nvme0n1          8-40498-00001        HITACHI SVOS-RF-System                   1           0.00   B /  10.74  GB    512   B +  0 B   A3042240",
        "/dev/nvme0n10         8-40498-00001        HITACHI SVOS-RF-System                   10          0.00   B /  10.74  GB    512   B +  0 B   A3042240",
        "/dev/nvme0n2          8-40498-00001        HITACHI SVOS-RF-System                   2           0.00   B /  10.74  GB    512   B +  0 B   A3042240",
        "/dev/nvme0n3          8-40498-00001        HITACHI SVOS-RF-System                   3           0.00   B /  10.74  GB    512   B +  0 B   A3042240",
        "/dev/nvme0n4          8-40498-00001        HITACHI SVOS-RF-System                   4           0.00   B /  10.74  GB    512   B +  0 B   A3042240",
        "/dev/nvme0n5          8-40498-00001        HITACHI SVOS-RF-System                   5           0.00   B /  10.74  GB    512   B +  0 B   A3042240",
        "/dev/nvme0n6          8-40498-00001        HITACHI SVOS-RF-System                   6           0.00   B /  10.74  GB    512   B +  0 B   A3042240",
        "/dev/nvme0n7          8-40498-00001        HITACHI SVOS-RF-System                   7           0.00   B /  10.74  GB    512   B +  0 B   A3042240",
        "/dev/nvme0n8          8-40498-00001        HITACHI SVOS-RF-System                   8           0.00   B /  10.74  GB    512   B +  0 B   A3042240",
        "/dev/nvme0n9          8-40498-00001        HITACHI SVOS-RF-System                   9           0.00   B /  10.74  GB    512   B +  0 B   A3042240"
    ]
}

TASK [roles/nvme_tcp_end_to_end_rhel : Step 5 - List NVMe subsystem paths] ***********************************************************
Thursday 02 April 2026  00:35:19 -0400 (0:00:00.017)       0:05:04.500 ******** 
Thursday 02 April 2026  00:35:19 -0400 (0:00:00.017)       0:05:04.499 ******** 
ok: [localhost -> 192.168.53.160]

TASK [roles/nvme_tcp_end_to_end_rhel : Step 5 - Display NVMe subsystem paths] ********************************************************
Thursday 02 April 2026  00:35:20 -0400 (0:00:01.214)       0:05:05.715 ******** 
Thursday 02 April 2026  00:35:20 -0400 (0:00:01.214)       0:05:05.714 ******** 
ok: [localhost] => {
    "nvme_subsys_result.stdout_lines": [
        "nvme-subsys0 - NQN=nqn.1994-04.jp.co.hitachi:nvme:storage-subsystem-sn.8-40498-nvmssid.00001",
        "\\",
        " +- nvme0 tcp traddr=192.168.10.30 trsvcid=4420 host_traddr=192.168.10.45 live ",
        " +- nvme1 tcp traddr=192.168.20.30 trsvcid=4420 host_traddr=192.168.20.45 live "
    ]
}

TASK [roles/nvme_tcp_end_to_end_rhel : Step 6 - Check current NVMe native multipath status] ******************************************
Thursday 02 April 2026  00:35:20 -0400 (0:00:00.016)       0:05:05.732 ******** 
Thursday 02 April 2026  00:35:20 -0400 (0:00:00.016)       0:05:05.730 ******** 
ok: [localhost -> 192.168.53.160]

TASK [roles/nvme_tcp_end_to_end_rhel : Step 6 - Display current multipath status] ****************************************************
Thursday 02 April 2026  00:35:21 -0400 (0:00:01.064)       0:05:06.796 ******** 
Thursday 02 April 2026  00:35:21 -0400 (0:00:01.064)       0:05:06.795 ******** 
ok: [localhost] => {
    "msg": "NVMe native multipath enabled: Y"
}

TASK [roles/nvme_tcp_end_to_end_rhel : Step 6 - Enable NVMe native multipath via grubby on ALL kernels (if not already enabled)] *****
Thursday 02 April 2026  00:35:21 -0400 (0:00:00.040)       0:05:06.837 ******** 
Thursday 02 April 2026  00:35:21 -0400 (0:00:00.040)       0:05:06.835 ******** 
skipping: [localhost]

TASK [roles/nvme_tcp_end_to_end_rhel : Step 6 - Create modprobe config for NVMe native multipath persistence] ************************
Thursday 02 April 2026  00:35:21 -0400 (0:00:00.032)       0:05:06.870 ******** 
Thursday 02 April 2026  00:35:21 -0400 (0:00:00.032)       0:05:06.868 ******** 
skipping: [localhost]

TASK [roles/nvme_tcp_end_to_end_rhel : Step 6 - Disable DM multipath (not needed with NVMe native multipath)] ************************
Thursday 02 April 2026  00:35:21 -0400 (0:00:00.033)       0:05:06.903 ******** 
Thursday 02 April 2026  00:35:21 -0400 (0:00:00.033)       0:05:06.902 ******** 
ok: [localhost -> 192.168.53.160]

TASK [roles/nvme_tcp_end_to_end_rhel : Step 6 - Remove /etc/multipath.conf if present] ***********************************************
Thursday 02 April 2026  00:35:22 -0400 (0:00:01.213)       0:05:08.117 ******** 
Thursday 02 April 2026  00:35:22 -0400 (0:00:01.213)       0:05:08.116 ******** 
ok: [localhost -> 192.168.53.160]

TASK [roles/nvme_tcp_end_to_end_rhel : Step 6 - Flush DM multipath maps] *************************************************************
Thursday 02 April 2026  00:35:23 -0400 (0:00:01.079)       0:05:09.196 ******** 
Thursday 02 April 2026  00:35:23 -0400 (0:00:01.079)       0:05:09.195 ******** 
ok: [localhost -> 192.168.53.160]

TASK [roles/nvme_tcp_end_to_end_rhel : Step 6 - Create udev rule for Hitachi SVOS round-robin IO policy] *****************************
Thursday 02 April 2026  00:35:25 -0400 (0:00:01.076)       0:05:10.272 ******** 
Thursday 02 April 2026  00:35:25 -0400 (0:00:01.076)       0:05:10.271 ******** 
ok: [localhost -> 192.168.53.160]

TASK [roles/nvme_tcp_end_to_end_rhel : Step 6 - Regenerate initramfs] ****************************************************************
Thursday 02 April 2026  00:35:26 -0400 (0:00:01.746)       0:05:12.019 ******** 
Thursday 02 April 2026  00:35:26 -0400 (0:00:01.746)       0:05:12.018 ******** 
skipping: [localhost]

TASK [roles/nvme_tcp_end_to_end_rhel : Step 6 - Display dracut result] ***************************************************************
Thursday 02 April 2026  00:35:26 -0400 (0:00:00.041)       0:05:12.060 ******** 
Thursday 02 April 2026  00:35:26 -0400 (0:00:00.041)       0:05:12.059 ******** 
skipping: [localhost]

TASK [roles/nvme_tcp_end_to_end_rhel : Step 6 - NOTICE - Reboot required if multipath was just enabled] ******************************
Thursday 02 April 2026  00:35:26 -0400 (0:00:00.031)       0:05:12.092 ******** 
Thursday 02 April 2026  00:35:26 -0400 (0:00:00.031)       0:05:12.091 ******** 
skipping: [localhost]

TASK [roles/nvme_tcp_end_to_end_rhel : Step 6 - Verify NVMe native multipath (if already enabled)] ***********************************
Thursday 02 April 2026  00:35:26 -0400 (0:00:00.023)       0:05:12.116 ******** 
Thursday 02 April 2026  00:35:26 -0400 (0:00:00.023)       0:05:12.114 ******** 
ok: [localhost] => {
    "msg": "NVMe native multipath is already enabled. No reboot required."
}

TASK [roles/nvme_tcp_end_to_end_rhel : Step 6 - Verify IO policy for NVMe subsystems (if multipath already active)] ******************
Thursday 02 April 2026  00:35:26 -0400 (0:00:00.027)       0:05:12.143 ******** 
Thursday 02 April 2026  00:35:26 -0400 (0:00:00.027)       0:05:12.142 ******** 
ok: [localhost -> 192.168.53.160]

TASK [roles/nvme_tcp_end_to_end_rhel : Step 6 - Display IO policy] *******************************************************************
Thursday 02 April 2026  00:35:28 -0400 (0:00:02.061)       0:05:14.205 ******** 
Thursday 02 April 2026  00:35:28 -0400 (0:00:02.061)       0:05:14.204 ******** 
ok: [localhost] => {
    "iopolicy_result.stdout_lines": [
        "round-robin"
    ]
}

TASK [roles/nvme_tcp_end_to_end_rhel : Step 6 - Final NVMe namespace and subsystem verification] *************************************
Thursday 02 April 2026  00:35:28 -0400 (0:00:00.020)       0:05:14.226 ******** 
Thursday 02 April 2026  00:35:28 -0400 (0:00:00.020)       0:05:14.225 ******** 
ok: [localhost -> 192.168.53.160]

TASK [roles/nvme_tcp_end_to_end_rhel : Step 6 - Display final NVMe namespace list] ***************************************************
Thursday 02 April 2026  00:35:30 -0400 (0:00:01.231)       0:05:15.458 ******** 
Thursday 02 April 2026  00:35:30 -0400 (0:00:01.231)       0:05:15.456 ******** 
ok: [localhost] => {
    "final_nvme_list.stdout_lines": [
        "Node                  SN                   Model                                    Namespace Usage                      Format           FW Rev  ",
        "--------------------- -------------------- ---------------------------------------- --------- -------------------------- ---------------- --------",
        "/dev/nvme0n1          8-40498-00001        HITACHI SVOS-RF-System                   1           0.00   B /  10.74  GB    512   B +  0 B   A3042240",
        "/dev/nvme0n10         8-40498-00001        HITACHI SVOS-RF-System                   10          0.00   B /  10.74  GB    512   B +  0 B   A3042240",
        "/dev/nvme0n2          8-40498-00001        HITACHI SVOS-RF-System                   2           0.00   B /  10.74  GB    512   B +  0 B   A3042240",
        "/dev/nvme0n3          8-40498-00001        HITACHI SVOS-RF-System                   3           0.00   B /  10.74  GB    512   B +  0 B   A3042240",
        "/dev/nvme0n4          8-40498-00001        HITACHI SVOS-RF-System                   4           0.00   B /  10.74  GB    512   B +  0 B   A3042240",
        "/dev/nvme0n5          8-40498-00001        HITACHI SVOS-RF-System                   5           0.00   B /  10.74  GB    512   B +  0 B   A3042240",
        "/dev/nvme0n6          8-40498-00001        HITACHI SVOS-RF-System                   6           0.00   B /  10.74  GB    512   B +  0 B   A3042240",
        "/dev/nvme0n7          8-40498-00001        HITACHI SVOS-RF-System                   7           0.00   B /  10.74  GB    512   B +  0 B   A3042240",
        "/dev/nvme0n8          8-40498-00001        HITACHI SVOS-RF-System                   8           0.00   B /  10.74  GB    512   B +  0 B   A3042240",
        "/dev/nvme0n9          8-40498-00001        HITACHI SVOS-RF-System                   9           0.00   B /  10.74  GB    512   B +  0 B   A3042240"
    ]
}

TASK [roles/nvme_tcp_end_to_end_rhel : Step 6 - Final NVMe subsystem path verification] **********************************************
Thursday 02 April 2026  00:35:30 -0400 (0:00:00.020)       0:05:15.478 ******** 
Thursday 02 April 2026  00:35:30 -0400 (0:00:00.020)       0:05:15.476 ******** 
ok: [localhost -> 192.168.53.160]

TASK [roles/nvme_tcp_end_to_end_rhel : Step 6 - Display final subsystem paths (multipath verification)] ******************************
Thursday 02 April 2026  00:35:31 -0400 (0:00:01.227)       0:05:16.705 ******** 
Thursday 02 April 2026  00:35:31 -0400 (0:00:01.227)       0:05:16.704 ******** 
ok: [localhost] => {
    "final_subsys_result.stdout_lines": [
        "nvme-subsys0 - NQN=nqn.1994-04.jp.co.hitachi:nvme:storage-subsystem-sn.8-40498-nvmssid.00001",
        "\\",
        " +- nvme0 tcp traddr=192.168.10.30 trsvcid=4420 host_traddr=192.168.10.45 live ",
        " +- nvme1 tcp traddr=192.168.20.30 trsvcid=4420 host_traddr=192.168.20.45 live "
    ]
}

PLAY RECAP ***************************************************************************************************************************
localhost                  : ok=56   changed=8    unreachable=0    failed=0    skipped=6    rescued=0    ignored=0   


TASKS RECAP **************************************************************************************************************************
Thursday 02 April 2026  00:35:31 -0400 (0:00:00.028)       0:05:16.734 ******** 
=============================================================================== 
roles/nvme_tcp_end_to_end_rhel : Step 1 - Create LDEVs for NVMe/TCP namespaces ---------------------------------------------- 126.85s
roles/nvme_tcp_end_to_end_rhel : Step 4 - Add namespaces and namespace paths to NVM Subsystem ------------------------------- 117.91s
roles/nvme_tcp_end_to_end_rhel : Step 3 - Create NVM Subsystem with ports and host NQN --------------------------------------- 28.73s
roles/nvme_tcp_end_to_end_rhel : Step 2 - Verify connectivity to storage port 1 ----------------------------------------------- 4.16s
roles/nvme_tcp_end_to_end_rhel : Step 2 - Verify connectivity to storage port 2 ----------------------------------------------- 4.14s
roles/nvme_tcp_end_to_end_rhel : Step 2 - Verify nvme-cli is installed -------------------------------------------------------- 3.00s
roles/nvme_tcp_end_to_end_rhel : Step 6 - Verify IO policy for NVMe subsystems (if multipath already active) ------------------ 2.06s
roles/nvme_tcp_end_to_end_rhel : Step 6 - Create udev rule for Hitachi SVOS round-robin IO policy ----------------------------- 1.75s
roles/nvme_tcp_end_to_end_rhel : Step 5 - Configure /etc/nvme/discovery.conf -------------------------------------------------- 1.73s
roles/nvme_tcp_end_to_end_rhel : Step 5 - Enable and start nvmf-autoconnect service ------------------------------------------- 1.70s
roles/nvme_tcp_end_to_end_rhel : Step 5 - Disconnect any stale NVMe-oF sessions ----------------------------------------------- 1.67s
roles/nvme_tcp_end_to_end_rhel : Step 5 - Load nvme_tcp kernel module --------------------------------------------------------- 1.57s
roles/nvme_tcp_end_to_end_rhel : Step 5 - List connected NVMe namespaces ------------------------------------------------------ 1.24s
roles/nvme_tcp_end_to_end_rhel : Step 6 - Final NVMe namespace and subsystem verification ------------------------------------- 1.23s
roles/nvme_tcp_end_to_end_rhel : Step 6 - Final NVMe subsystem path verification ---------------------------------------------- 1.23s
roles/nvme_tcp_end_to_end_rhel : Step 5 - List NVMe subsystem paths ----------------------------------------------------------- 1.21s
roles/nvme_tcp_end_to_end_rhel : Step 6 - Disable DM multipath (not needed with NVMe native multipath) ------------------------ 1.21s
roles/nvme_tcp_end_to_end_rhel : Step 2 - Configure static IP on NIC interface 1 (ens97f1) ------------------------------------ 1.13s
roles/nvme_tcp_end_to_end_rhel : Step 5 - Connect to NVMe subsystem via storage port 1 ---------------------------------------- 1.13s
roles/nvme_tcp_end_to_end_rhel : Step 2 - Configure static IP on NIC interface 2 (ens99f1) ------------------------------------ 1.11s

ROLES RECAP **************************************************************************************************************************
Thursday 02 April 2026  00:35:31 -0400 (0:00:00.028)       0:05:16.733 ******** 
=============================================================================== 
roles/nvme_tcp_end_to_end_rhel ---------------------------------------- 316.70s
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~ 
total ----------------------------------------------------------------- 316.70s
visubramaniam@MQ7HY4M9M0 visa_demo % 