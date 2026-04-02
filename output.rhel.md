visubramaniam@MQ7HY4M9M0 visa_demo % ansible-playbook site_rhel.yml
[WARNING]: No inventory was parsed, only implicit localhost is available
[WARNING]: provided hosts list is empty, only localhost is available. Note that the implicit localhost does not match 'all'

PLAY [NVMe/TCP End-to-End Setup: VSP One Block 28 + RHEL] ****************************************************************************

TASK [roles/nvme_tcp_end_to_end_rhel : Step 1 - Create LDEVs for NVMe/TCP namespaces] ************************************************
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
[WARNING]: Host 'localhost' is using the discovered Python interpreter at '/usr/bin/python3.12', but future installation of another Python interpreter could cause a different interpreter to be discovered. See https://docs.ansible.com/ansible-core/2.20/reference_appendices/interpreter_discovery.html for more information.
ok: [localhost -> 192.168.53.160]

TASK [roles/nvme_tcp_end_to_end_rhel : Step 2 - Install nvme-cli if not present] *****************************************************
skipping: [localhost]

TASK [roles/nvme_tcp_end_to_end_rhel : Step 2 - Display installed nvme-cli package] **************************************************
ok: [localhost] => {
    "msg": "nvme-cli: ['nvme-cli-1.16-9.el8.x86_64']"
}

TASK [roles/nvme_tcp_end_to_end_rhel : Step 2 - Read host NQN from RHEL host] ********************************************************
ok: [localhost -> 192.168.53.160]

TASK [roles/nvme_tcp_end_to_end_rhel : Step 2 - Set host NQN fact for use in Steps 3 and 4] ******************************************
ok: [localhost]

TASK [roles/nvme_tcp_end_to_end_rhel : Step 2 - Display RHEL host NQN] ***************************************************************
ok: [localhost] => {
    "msg": "RHEL Host NQN: nqn.2014-08.org.nvmexpress:uuid:ca845a3c-fe2f-4e6a-96dd-99b094774113"
}

TASK [roles/nvme_tcp_end_to_end_rhel : Step 2 - Configure static IP on NIC interface 1 (ens97f1)] ************************************
changed: [localhost -> 192.168.53.160]

TASK [roles/nvme_tcp_end_to_end_rhel : Step 2 - Configure static IP on NIC interface 2 (ens99f1)] ************************************
changed: [localhost -> 192.168.53.160]

TASK [roles/nvme_tcp_end_to_end_rhel : Step 2 - Verify NIC interface IP addresses] ***************************************************
ok: [localhost -> 192.168.53.160]

TASK [roles/nvme_tcp_end_to_end_rhel : Step 2 - Display NIC IP addresses] ************************************************************
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
        "    inet 192.168.53.160/22 brd 192.168.55.255 scope global noprefixroute ens8f0",
        "       valid_lft forever preferred_lft forever",
        "    inet6 fd01:52::f2b2:b9ff:fe16:a478/64 scope global dynamic noprefixroute ",
        "       valid_lft 2591907sec preferred_lft 604707sec",
        "    inet6 fe80::f2b2:b9ff:fe16:a478/64 scope link noprefixroute ",
        "       valid_lft forever preferred_lft forever",
        "3: ens8f1: <NO-CARRIER,BROADCAST,MULTICAST,UP> mtu 1500 qdisc mq state DOWN group default qlen 1000",
        "    link/ether f0:b2:b9:16:a4:79 brd ff:ff:ff:ff:ff:ff",
        "4: ens8f2: <NO-CARRIER,BROADCAST,MULTICAST,UP> mtu 1500 qdisc mq state DOWN group default qlen 1000",
        "    link/ether f0:b2:b9:16:a4:7a brd ff:ff:ff:ff:ff:ff",
        "5: ens8f3: <NO-CARRIER,BROADCAST,MULTICAST,UP> mtu 1500 qdisc mq state DOWN group default qlen 1000",
        "    link/ether f0:b2:b9:16:a4:7b brd ff:ff:ff:ff:ff:ff",
        "6: ens97f0: <NO-CARRIER,BROADCAST,MULTICAST,UP> mtu 1500 qdisc mq state DOWN group default qlen 1000",
        "    link/ether 58:a2:e1:11:f5:5c brd ff:ff:ff:ff:ff:ff",
        "7: ens97f1: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc mq state UP group default qlen 1000",
        "    link/ether 58:a2:e1:11:f5:5d brd ff:ff:ff:ff:ff:ff",
        "    inet 192.168.10.45/24 brd 192.168.10.255 scope global noprefixroute ens97f1",
        "       valid_lft forever preferred_lft forever",
        "    inet6 fe80::d4e9:6b96:406a:bb54/64 scope link noprefixroute ",
        "       valid_lft forever preferred_lft forever",
        "8: ens45f0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc mq state UP group default qlen 1000",
        "    link/ether 9c:63:c0:95:17:56 brd ff:ff:ff:ff:ff:ff",
        "    inet 172.28.53.160/16 brd 172.28.255.255 scope global noprefixroute ens45f0",
        "       valid_lft forever preferred_lft forever",
        "    inet6 fd01:52::9e63:c0ff:fe95:1756/64 scope global dynamic mngtmpaddr ",
        "       valid_lft 2591906sec preferred_lft 604706sec",
        "    inet6 fe80::9e63:c0ff:fe95:1756/64 scope link ",
        "       valid_lft forever preferred_lft forever",
        "9: ens45f1: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc mq state UP group default qlen 1000",
        "    link/ether 9c:63:c0:95:17:57 brd ff:ff:ff:ff:ff:ff",
        "    inet 172.29.53.160/16 brd 172.29.255.255 scope global noprefixroute ens45f1",
        "       valid_lft forever preferred_lft forever",
        "    inet6 fd01:52::9e63:c0ff:fe95:1757/64 scope global dynamic mngtmpaddr ",
        "       valid_lft 2591906sec preferred_lft 604706sec",
        "    inet6 fe80::9e63:c0ff:fe95:1757/64 scope link ",
        "       valid_lft forever preferred_lft forever",
        "10: ens99f0: <NO-CARRIER,BROADCAST,MULTICAST,UP> mtu 1500 qdisc mq state DOWN group default qlen 1000",
        "    link/ether 58:a2:e1:12:0c:6c brd ff:ff:ff:ff:ff:ff",
        "11: ens99f1: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc mq state UP group default qlen 1000",
        "    link/ether 58:a2:e1:12:0c:6d brd ff:ff:ff:ff:ff:ff",
        "    inet 192.168.20.45/24 brd 192.168.20.255 scope global noprefixroute ens99f1",
        "       valid_lft forever preferred_lft forever",
        "    inet6 fe80::9f1:6708:aa89:c2ed/64 scope link tentative noprefixroute ",
        "       valid_lft forever preferred_lft forever",
        "12: usb0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UNKNOWN group default qlen 1000",
        "    link/ether ea:22:27:f4:67:70 brd ff:ff:ff:ff:ff:ff"
    ]
}

TASK [roles/nvme_tcp_end_to_end_rhel : Step 2 - Verify connectivity to storage port 1] ***********************************************
ok: [localhost -> 192.168.53.160]

TASK [roles/nvme_tcp_end_to_end_rhel : Step 2 - Verify connectivity to storage port 2] ***********************************************
ok: [localhost -> 192.168.53.160]

TASK [roles/nvme_tcp_end_to_end_rhel : Step 2 - Display connectivity results] ********************************************************
ok: [localhost] => {
    "msg": [
        "Ping to 192.168.10.30: SUCCESS",
        "Ping to 192.168.20.30: SUCCESS"
    ]
}

TASK [roles/nvme_tcp_end_to_end_rhel : Step 3 - Create NVM Subsystem with ports and host NQN] ****************************************
changed: [localhost]

TASK [roles/nvme_tcp_end_to_end_rhel : Step 3 - Display NVM Subsystem creation result] ***********************************************
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
ok: [localhost]

TASK [roles/nvme_tcp_end_to_end_rhel : Step 3 - Construct subsystem NQN] *************************************************************
ok: [localhost]

TASK [roles/nvme_tcp_end_to_end_rhel : Step 3 - Save subsystem NQN to generated vars file] *******************************************
ok: [localhost]

TASK [roles/nvme_tcp_end_to_end_rhel : Step 3 - Display constructed subsystem NQN] ***************************************************
ok: [localhost] => {
    "msg": "Subsystem NQN saved: nqn.1994-04.jp.co.hitachi:nvme:storage-subsystem-sn.8-40498-nvmssid.00001"
}

TASK [roles/nvme_tcp_end_to_end_rhel : Step 4 - Add namespaces and namespace paths to NVM Subsystem] *********************************
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
changed: [localhost -> 192.168.53.160]

TASK [roles/nvme_tcp_end_to_end_rhel : Step 5 - Verify nvme_tcp module is loaded] ****************************************************
ok: [localhost -> 192.168.53.160]

TASK [roles/nvme_tcp_end_to_end_rhel : Step 5 - Display nvme_tcp module status] ******************************************************
ok: [localhost] => {
    "lsmod_result.stdout_lines": [
        "nvme_tcp               32768  0",
        "nvme_fabrics           24576  1 nvme_tcp",
        "nvme_core             110592  2 nvme_tcp,nvme_fabrics"
    ]
}

TASK [roles/nvme_tcp_end_to_end_rhel : Step 5 - Check if auto-generated NQN file exists] *********************************************
ok: [localhost]

TASK [roles/nvme_tcp_end_to_end_rhel : Step 5 - Load auto-generated subsystem NQN] ***************************************************
ok: [localhost]

TASK [roles/nvme_tcp_end_to_end_rhel : Step 5 - Display subsystem NQN being used] ****************************************************
ok: [localhost] => {
    "msg": "Using subsystem NQN: nqn.1994-04.jp.co.hitachi:nvme:storage-subsystem-sn.8-40498-nvmssid.00001"
}

TASK [roles/nvme_tcp_end_to_end_rhel : Step 5 - Discover NVMe targets via storage port 1] ********************************************
ok: [localhost -> 192.168.53.160]

TASK [roles/nvme_tcp_end_to_end_rhel : Step 5 - Display discovery results for storage port 1] ****************************************
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
ok: [localhost -> 192.168.53.160]

TASK [roles/nvme_tcp_end_to_end_rhel : Step 5 - Display discovery results for storage port 2] ****************************************
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
ok: [localhost -> 192.168.53.160]

TASK [roles/nvme_tcp_end_to_end_rhel : Step 5 - Disconnect any stale NVMe-oF sessions] ***********************************************
ok: [localhost -> 192.168.53.160]

TASK [roles/nvme_tcp_end_to_end_rhel : Step 5 - Connect to NVMe subsystem via storage port 1] ****************************************
changed: [localhost -> 192.168.53.160]

TASK [roles/nvme_tcp_end_to_end_rhel : Step 5 - Display connect port 1 result] *******************************************************
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
        "delta": "0:00:00.057640",
        "end": "2026-04-01 23:34:12.969226",
        "failed": false,
        "msg": "",
        "rc": 0,
        "start": "2026-04-01 23:34:12.911586",
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
changed: [localhost -> 192.168.53.160]

TASK [roles/nvme_tcp_end_to_end_rhel : Step 5 - Display connect port 2 result] *******************************************************
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
        "delta": "0:00:00.049052",
        "end": "2026-04-01 23:34:14.145100",
        "failed": false,
        "msg": "",
        "rc": 0,
        "start": "2026-04-01 23:34:14.096048",
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
changed: [localhost -> 192.168.53.160]

TASK [roles/nvme_tcp_end_to_end_rhel : Step 5 - List connected NVMe namespaces] ******************************************************
ok: [localhost -> 192.168.53.160]

TASK [roles/nvme_tcp_end_to_end_rhel : Step 5 - Display NVMe namespaces] *************************************************************
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
        "/dev/nvme0n9          8-40498-00001        HITACHI SVOS-RF-System                   9           0.00   B /  10.74  GB    512   B +  0 B   A3042240",
        "/dev/nvme1n1          8-40498-00001        HITACHI SVOS-RF-System                   1           0.00   B /  10.74  GB    512   B +  0 B   A3042240",
        "/dev/nvme1n10         8-40498-00001        HITACHI SVOS-RF-System                   10          0.00   B /  10.74  GB    512   B +  0 B   A3042240",
        "/dev/nvme1n2          8-40498-00001        HITACHI SVOS-RF-System                   2           0.00   B /  10.74  GB    512   B +  0 B   A3042240",
        "/dev/nvme1n3          8-40498-00001        HITACHI SVOS-RF-System                   3           0.00   B /  10.74  GB    512   B +  0 B   A3042240",
        "/dev/nvme1n4          8-40498-00001        HITACHI SVOS-RF-System                   4           0.00   B /  10.74  GB    512   B +  0 B   A3042240",
        "/dev/nvme1n5          8-40498-00001        HITACHI SVOS-RF-System                   5           0.00   B /  10.74  GB    512   B +  0 B   A3042240",
        "/dev/nvme1n6          8-40498-00001        HITACHI SVOS-RF-System                   6           0.00   B /  10.74  GB    512   B +  0 B   A3042240",
        "/dev/nvme1n7          8-40498-00001        HITACHI SVOS-RF-System                   7           0.00   B /  10.74  GB    512   B +  0 B   A3042240",
        "/dev/nvme1n8          8-40498-00001        HITACHI SVOS-RF-System                   8           0.00   B /  10.74  GB    512   B +  0 B   A3042240",
        "/dev/nvme1n9          8-40498-00001        HITACHI SVOS-RF-System                   9           0.00   B /  10.74  GB    512   B +  0 B   A3042240"
    ]
}

TASK [roles/nvme_tcp_end_to_end_rhel : Step 5 - List NVMe subsystem paths] ***********************************************************
ok: [localhost -> 192.168.53.160]

TASK [roles/nvme_tcp_end_to_end_rhel : Step 5 - Display NVMe subsystem paths] ********************************************************
ok: [localhost] => {
    "nvme_subsys_result.stdout_lines": [
        "nvme-subsys0 - NQN=nqn.1994-04.jp.co.hitachi:nvme:storage-subsystem-sn.8-40498-nvmssid.00001",
        "\\",
        " +- nvme0 tcp traddr=192.168.10.30 trsvcid=4420 host_traddr=192.168.10.45 live ",
        " +- nvme1 tcp traddr=192.168.20.30 trsvcid=4420 host_traddr=192.168.20.45 live "
    ]
}

TASK [roles/nvme_tcp_end_to_end_rhel : Step 6 - Check current NVMe native multipath status] ******************************************
ok: [localhost -> 192.168.53.160]

TASK [roles/nvme_tcp_end_to_end_rhel : Step 6 - Display current multipath status] ****************************************************
ok: [localhost] => {
    "msg": "NVMe native multipath enabled: N"
}

TASK [roles/nvme_tcp_end_to_end_rhel : Step 6 - Enable NVMe native multipath via grubby (if not already enabled)] ********************
changed: [localhost -> 192.168.53.160]

TASK [roles/nvme_tcp_end_to_end_rhel : Step 6 - Disable DM multipath (not needed with NVMe native multipath)] ************************
ok: [localhost -> 192.168.53.160]

TASK [roles/nvme_tcp_end_to_end_rhel : Step 6 - Remove /etc/multipath.conf if present] ***********************************************
ok: [localhost -> 192.168.53.160]

TASK [roles/nvme_tcp_end_to_end_rhel : Step 6 - Flush DM multipath maps] *************************************************************
ok: [localhost -> 192.168.53.160]

TASK [roles/nvme_tcp_end_to_end_rhel : Step 6 - Create udev rule for Hitachi SVOS round-robin IO policy] *****************************
ok: [localhost -> 192.168.53.160]

TASK [roles/nvme_tcp_end_to_end_rhel : Step 6 - Regenerate initramfs] ****************************************************************
changed: [localhost -> 192.168.53.160]

TASK [roles/nvme_tcp_end_to_end_rhel : Step 6 - Display dracut result] ***************************************************************
ok: [localhost] => {
    "dracut_result": {
        "changed": true,
        "cmd": [
            "dracut",
            "-f",
            "-v"
        ],
        "delta": "0:00:12.133474",
        "end": "2026-04-01 23:34:39.331505",
        "failed": false,
        "msg": "",
        "rc": 0,
        "start": "2026-04-01 23:34:27.198031",
        "stderr": "dracut: Executing: /usr/bin/dracut -f -v\ndracut: dracut module 'busybox' will not be installed, because command 'busybox' could not be found!\ndracut: dracut module 'rngd' will not be installed, because command 'rngd' could not be found!\ndracut: dracut module 'btrfs' will not be installed, because command 'btrfs' could not be found!\ndracut: dracut module 'dmraid' will not be installed, because command 'dmraid' could not be found!\ndracut: 95nfs: Could not find any command of 'rpcbind portmap'!\ndracut: memstrack is available\ndracut: dracut module 'busybox' will not be installed, because command 'busybox' could not be found!\ndracut: dracut module 'rngd' will not be installed, because command 'rngd' could not be found!\ndracut: dracut module 'btrfs' will not be installed, because command 'btrfs' could not be found!\ndracut: dracut module 'dmraid' will not be installed, because command 'dmraid' could not be found!\ndracut: 95nfs: Could not find any command of 'rpcbind portmap'!\ndracut: *** Including module: bash ***\ndracut: *** Including module: systemd ***\ndracut: *** Including module: fips ***\ndracut: *** Including module: systemd-initrd ***\ndracut: *** Including module: nss-softokn ***\ndracut: *** Including module: i18n ***\ndracut: *** Including module: network-manager ***\ndracut: *** Including module: network ***\ndracut: *** Including module: ifcfg ***\ndracut: *** Including module: drm ***\ndracut: *** Including module: plymouth ***\ndracut: *** Including module: prefixdevname ***\ndracut: *** Including module: dm ***\ndracut: Skipping udev rule: 64-device-mapper.rules\ndracut: Skipping udev rule: 60-persistent-storage-dm.rules\ndracut: Skipping udev rule: 55-dm.rules\ndracut: *** Including module: kernel-modules ***\ndracut: *** Including module: kernel-modules-extra ***\ndracut: *** Including module: kernel-network-modules ***\ndracut: *** Including module: lvm ***\ndracut: Skipping udev rule: 64-device-mapper.rules\ndracut: Skipping udev rule: 56-lvm.rules\ndracut: Skipping udev rule: 60-persistent-storage-lvm.rules\ndracut: *** Including module: resume ***\ndracut: *** Including module: rootfs-block ***\ndracut: *** Including module: terminfo ***\ndracut: *** Including module: udev-rules ***\ndracut: Skipping udev rule: 91-permissions.rules\ndracut: Skipping udev rule: 80-drivers-modprobe.rules\ndracut: *** Including module: biosdevname ***\ndracut: *** Including module: dracut-systemd ***\ndracut: *** Including module: usrmount ***\ndracut: *** Including module: base ***\ndracut: *** Including module: fs-lib ***\ndracut: *** Including module: memstrack ***\ndracut: *** Including module: microcode_ctl-fw_dir_override ***\ndracut:   microcode_ctl module: mangling fw_dir\ndracut:     microcode_ctl: reset fw_dir to \"/lib/firmware/updates /lib/firmware\"\ndracut:     microcode_ctl: processing data directory  \"/usr/share/microcode_ctl/ucode_with_caveats/intel\"...\nintel: model '', path ' intel-ucode/*', kvers ''\ndracut:       microcode_ctl: intel: caveats check for kernel version \"4.18.0-305.25.1.el8_4.x86_64\" passed, adding \"/usr/share/microcode_ctl/ucode_with_caveats/intel\" to fw_dir variable\ndracut:     microcode_ctl: processing data directory  \"/usr/share/microcode_ctl/ucode_with_caveats/intel-06-2d-07\"...\nintel-06-2d-07: model 'GenuineIntel 06-2d-07', path ' intel-ucode/06-2d-07', kvers ''\nCurrent CPU model 'GenuineIntel 06-6a-06' doesn't match configuration CPU model 'GenuineIntel 06-2d-07', skipping\ndracut:     microcode_ctl: configuration \"intel-06-2d-07\" is ignored\ndracut:     microcode_ctl: processing data directory  \"/usr/share/microcode_ctl/ucode_with_caveats/intel-06-4e-03\"...\nintel-06-4e-03: model 'GenuineIntel 06-4e-03', path ' intel-ucode/06-4e-03', kvers ''\nCurrent CPU model 'GenuineIntel 06-6a-06' doesn't match configuration CPU model 'GenuineIntel 06-4e-03', skipping\ndracut:     microcode_ctl: configuration \"intel-06-4e-03\" is ignored\ndracut:     microcode_ctl: processing data directory  \"/usr/share/microcode_ctl/ucode_with_caveats/intel-06-4f-01\"...\nintel-06-4f-01: model 'GenuineIntel 06-4f-01', path ' intel-ucode/06-4f-01', kvers ' 4.17.0 3.10.0-894 3.10.0-862.6.1 3.10.0-693.35.1 3.10.0-514.52.1 3.10.0-327.70.1 2.6.32-754.1.1 2.6.32-573.58.1 2.6.32-504.71.1 2.6.32-431.90.1 2.6.32-358.90.1'\nCurrent CPU model 'GenuineIntel 06-6a-06' doesn't match configuration CPU model 'GenuineIntel 06-4f-01', skipping\ndracut:     microcode_ctl: configuration \"intel-06-4f-01\" is ignored\ndracut:     microcode_ctl: processing data directory  \"/usr/share/microcode_ctl/ucode_with_caveats/intel-06-55-04\"...\nintel-06-55-04: model 'GenuineIntel 06-55-04', path ' intel-ucode/06-55-04', kvers ''\nCurrent CPU model 'GenuineIntel 06-6a-06' doesn't match configuration CPU model 'GenuineIntel 06-55-04', skipping\ndracut:     microcode_ctl: configuration \"intel-06-55-04\" is ignored\ndracut:     microcode_ctl: processing data directory  \"/usr/share/microcode_ctl/ucode_with_caveats/intel-06-5e-03\"...\nintel-06-5e-03: model 'GenuineIntel 06-5e-03', path ' intel-ucode/06-5e-03', kvers ''\nCurrent CPU model 'GenuineIntel 06-6a-06' doesn't match configuration CPU model 'GenuineIntel 06-5e-03', skipping\ndracut:     microcode_ctl: configuration \"intel-06-5e-03\" is ignored\ndracut:     microcode_ctl: processing data directory  \"/usr/share/microcode_ctl/ucode_with_caveats/intel-06-8c-01\"...\nintel-06-8c-01: model 'GenuineIntel 06-8c-01', path ' intel-ucode/06-8c-01', kvers ''\nCurrent CPU model 'GenuineIntel 06-6a-06' doesn't match configuration CPU model 'GenuineIntel 06-8c-01', skipping\ndracut:     microcode_ctl: configuration \"intel-06-8c-01\" is ignored\ndracut:     microcode_ctl: processing data directory  \"/usr/share/microcode_ctl/ucode_with_caveats/intel-06-8e-9e-0x-0xca\"...\nintel-06-8e-9e-0x-0xca: model '', path ' intel-ucode/*', kvers ''\nNo matching microcode files in ' intel-ucode/*' for CPU model 'GenuineIntel 06-6a-06', skipping\ndracut:     microcode_ctl: configuration \"intel-06-8e-9e-0x-0xca\" is ignored\ndracut:     microcode_ctl: processing data directory  \"/usr/share/microcode_ctl/ucode_with_caveats/intel-06-8e-9e-0x-dell\"...\nintel-06-8e-9e-0x-dell: model '', path ' intel-ucode/*', kvers ''\nNo matching microcode files in ' intel-ucode/*' for CPU model 'GenuineIntel 06-6a-06', skipping\ndracut:     microcode_ctl: configuration \"intel-06-8e-9e-0x-dell\" is ignored\ndracut:     microcode_ctl: processing data directory  \"/usr/share/microcode_ctl/ucode_with_caveats/intel-06-8f-08\"...\nintel-06-8f-08: model 'GenuineIntel 06-8f-08', path ' intel-ucode/06-8f-08', kvers ''\nCurrent CPU model 'GenuineIntel 06-6a-06' doesn't match configuration CPU model 'GenuineIntel 06-8f-08', skipping\ndracut:     microcode_ctl: configuration \"intel-06-8f-08\" is ignored\ndracut:     microcode_ctl: final fw_dir: \"/usr/share/microcode_ctl/ucode_with_caveats/intel /lib/firmware/updates /lib/firmware\"\ndracut: *** Including module: shutdown ***\ndracut: *** Including modules done ***\ndracut: *** Installing kernel module dependencies ***\ndracut: *** Installing kernel module dependencies done ***\ndracut: *** Resolving executable dependencies ***\ndracut: *** Resolving executable dependencies done***\ndracut: *** Hardlinking files ***\ndracut: *** Hardlinking files done ***\ndracut: *** Generating early-microcode cpio image ***\ndracut: *** Constructing GenuineIntel.bin ***\ndracut: *** Store current command line parameters ***\ndracut: *** Creating image file '/boot/initramfs-4.18.0-305.25.1.el8_4.x86_64.img' ***\ndracut: *** Creating initramfs image file '/boot/initramfs-4.18.0-305.25.1.el8_4.x86_64.img' done ***",
        "stderr_lines": [
            "dracut: Executing: /usr/bin/dracut -f -v",
            "dracut: dracut module 'busybox' will not be installed, because command 'busybox' could not be found!",
            "dracut: dracut module 'rngd' will not be installed, because command 'rngd' could not be found!",
            "dracut: dracut module 'btrfs' will not be installed, because command 'btrfs' could not be found!",
            "dracut: dracut module 'dmraid' will not be installed, because command 'dmraid' could not be found!",
            "dracut: 95nfs: Could not find any command of 'rpcbind portmap'!",
            "dracut: memstrack is available",
            "dracut: dracut module 'busybox' will not be installed, because command 'busybox' could not be found!",
            "dracut: dracut module 'rngd' will not be installed, because command 'rngd' could not be found!",
            "dracut: dracut module 'btrfs' will not be installed, because command 'btrfs' could not be found!",
            "dracut: dracut module 'dmraid' will not be installed, because command 'dmraid' could not be found!",
            "dracut: 95nfs: Could not find any command of 'rpcbind portmap'!",
            "dracut: *** Including module: bash ***",
            "dracut: *** Including module: systemd ***",
            "dracut: *** Including module: fips ***",
            "dracut: *** Including module: systemd-initrd ***",
            "dracut: *** Including module: nss-softokn ***",
            "dracut: *** Including module: i18n ***",
            "dracut: *** Including module: network-manager ***",
            "dracut: *** Including module: network ***",
            "dracut: *** Including module: ifcfg ***",
            "dracut: *** Including module: drm ***",
            "dracut: *** Including module: plymouth ***",
            "dracut: *** Including module: prefixdevname ***",
            "dracut: *** Including module: dm ***",
            "dracut: Skipping udev rule: 64-device-mapper.rules",
            "dracut: Skipping udev rule: 60-persistent-storage-dm.rules",
            "dracut: Skipping udev rule: 55-dm.rules",
            "dracut: *** Including module: kernel-modules ***",
            "dracut: *** Including module: kernel-modules-extra ***",
            "dracut: *** Including module: kernel-network-modules ***",
            "dracut: *** Including module: lvm ***",
            "dracut: Skipping udev rule: 64-device-mapper.rules",
            "dracut: Skipping udev rule: 56-lvm.rules",
            "dracut: Skipping udev rule: 60-persistent-storage-lvm.rules",
            "dracut: *** Including module: resume ***",
            "dracut: *** Including module: rootfs-block ***",
            "dracut: *** Including module: terminfo ***",
            "dracut: *** Including module: udev-rules ***",
            "dracut: Skipping udev rule: 91-permissions.rules",
            "dracut: Skipping udev rule: 80-drivers-modprobe.rules",
            "dracut: *** Including module: biosdevname ***",
            "dracut: *** Including module: dracut-systemd ***",
            "dracut: *** Including module: usrmount ***",
            "dracut: *** Including module: base ***",
            "dracut: *** Including module: fs-lib ***",
            "dracut: *** Including module: memstrack ***",
            "dracut: *** Including module: microcode_ctl-fw_dir_override ***",
            "dracut:   microcode_ctl module: mangling fw_dir",
            "dracut:     microcode_ctl: reset fw_dir to \"/lib/firmware/updates /lib/firmware\"",
            "dracut:     microcode_ctl: processing data directory  \"/usr/share/microcode_ctl/ucode_with_caveats/intel\"...",
            "intel: model '', path ' intel-ucode/*', kvers ''",
            "dracut:       microcode_ctl: intel: caveats check for kernel version \"4.18.0-305.25.1.el8_4.x86_64\" passed, adding \"/usr/share/microcode_ctl/ucode_with_caveats/intel\" to fw_dir variable",
            "dracut:     microcode_ctl: processing data directory  \"/usr/share/microcode_ctl/ucode_with_caveats/intel-06-2d-07\"...",
            "intel-06-2d-07: model 'GenuineIntel 06-2d-07', path ' intel-ucode/06-2d-07', kvers ''",
            "Current CPU model 'GenuineIntel 06-6a-06' doesn't match configuration CPU model 'GenuineIntel 06-2d-07', skipping",
            "dracut:     microcode_ctl: configuration \"intel-06-2d-07\" is ignored",
            "dracut:     microcode_ctl: processing data directory  \"/usr/share/microcode_ctl/ucode_with_caveats/intel-06-4e-03\"...",
            "intel-06-4e-03: model 'GenuineIntel 06-4e-03', path ' intel-ucode/06-4e-03', kvers ''",
            "Current CPU model 'GenuineIntel 06-6a-06' doesn't match configuration CPU model 'GenuineIntel 06-4e-03', skipping",
            "dracut:     microcode_ctl: configuration \"intel-06-4e-03\" is ignored",
            "dracut:     microcode_ctl: processing data directory  \"/usr/share/microcode_ctl/ucode_with_caveats/intel-06-4f-01\"...",
            "intel-06-4f-01: model 'GenuineIntel 06-4f-01', path ' intel-ucode/06-4f-01', kvers ' 4.17.0 3.10.0-894 3.10.0-862.6.1 3.10.0-693.35.1 3.10.0-514.52.1 3.10.0-327.70.1 2.6.32-754.1.1 2.6.32-573.58.1 2.6.32-504.71.1 2.6.32-431.90.1 2.6.32-358.90.1'",
            "Current CPU model 'GenuineIntel 06-6a-06' doesn't match configuration CPU model 'GenuineIntel 06-4f-01', skipping",
            "dracut:     microcode_ctl: configuration \"intel-06-4f-01\" is ignored",
            "dracut:     microcode_ctl: processing data directory  \"/usr/share/microcode_ctl/ucode_with_caveats/intel-06-55-04\"...",
            "intel-06-55-04: model 'GenuineIntel 06-55-04', path ' intel-ucode/06-55-04', kvers ''",
            "Current CPU model 'GenuineIntel 06-6a-06' doesn't match configuration CPU model 'GenuineIntel 06-55-04', skipping",
            "dracut:     microcode_ctl: configuration \"intel-06-55-04\" is ignored",
            "dracut:     microcode_ctl: processing data directory  \"/usr/share/microcode_ctl/ucode_with_caveats/intel-06-5e-03\"...",
            "intel-06-5e-03: model 'GenuineIntel 06-5e-03', path ' intel-ucode/06-5e-03', kvers ''",
            "Current CPU model 'GenuineIntel 06-6a-06' doesn't match configuration CPU model 'GenuineIntel 06-5e-03', skipping",
            "dracut:     microcode_ctl: configuration \"intel-06-5e-03\" is ignored",
            "dracut:     microcode_ctl: processing data directory  \"/usr/share/microcode_ctl/ucode_with_caveats/intel-06-8c-01\"...",
            "intel-06-8c-01: model 'GenuineIntel 06-8c-01', path ' intel-ucode/06-8c-01', kvers ''",
            "Current CPU model 'GenuineIntel 06-6a-06' doesn't match configuration CPU model 'GenuineIntel 06-8c-01', skipping",
            "dracut:     microcode_ctl: configuration \"intel-06-8c-01\" is ignored",
            "dracut:     microcode_ctl: processing data directory  \"/usr/share/microcode_ctl/ucode_with_caveats/intel-06-8e-9e-0x-0xca\"...",
            "intel-06-8e-9e-0x-0xca: model '', path ' intel-ucode/*', kvers ''",
            "No matching microcode files in ' intel-ucode/*' for CPU model 'GenuineIntel 06-6a-06', skipping",
            "dracut:     microcode_ctl: configuration \"intel-06-8e-9e-0x-0xca\" is ignored",
            "dracut:     microcode_ctl: processing data directory  \"/usr/share/microcode_ctl/ucode_with_caveats/intel-06-8e-9e-0x-dell\"...",
            "intel-06-8e-9e-0x-dell: model '', path ' intel-ucode/*', kvers ''",
            "No matching microcode files in ' intel-ucode/*' for CPU model 'GenuineIntel 06-6a-06', skipping",
            "dracut:     microcode_ctl: configuration \"intel-06-8e-9e-0x-dell\" is ignored",
            "dracut:     microcode_ctl: processing data directory  \"/usr/share/microcode_ctl/ucode_with_caveats/intel-06-8f-08\"...",
            "intel-06-8f-08: model 'GenuineIntel 06-8f-08', path ' intel-ucode/06-8f-08', kvers ''",
            "Current CPU model 'GenuineIntel 06-6a-06' doesn't match configuration CPU model 'GenuineIntel 06-8f-08', skipping",
            "dracut:     microcode_ctl: configuration \"intel-06-8f-08\" is ignored",
            "dracut:     microcode_ctl: final fw_dir: \"/usr/share/microcode_ctl/ucode_with_caveats/intel /lib/firmware/updates /lib/firmware\"",
            "dracut: *** Including module: shutdown ***",
            "dracut: *** Including modules done ***",
            "dracut: *** Installing kernel module dependencies ***",
            "dracut: *** Installing kernel module dependencies done ***",
            "dracut: *** Resolving executable dependencies ***",
            "dracut: *** Resolving executable dependencies done***",
            "dracut: *** Hardlinking files ***",
            "dracut: *** Hardlinking files done ***",
            "dracut: *** Generating early-microcode cpio image ***",
            "dracut: *** Constructing GenuineIntel.bin ***",
            "dracut: *** Store current command line parameters ***",
            "dracut: *** Creating image file '/boot/initramfs-4.18.0-305.25.1.el8_4.x86_64.img' ***",
            "dracut: *** Creating initramfs image file '/boot/initramfs-4.18.0-305.25.1.el8_4.x86_64.img' done ***"
        ],
        "stdout": "",
        "stdout_lines": [],
        "warnings": [
            "Host 'localhost' is using the discovered Python interpreter at '/usr/bin/python3.12', but future installation of another Python interpreter could cause a different interpreter to be discovered."
        ]
    }
}

TASK [roles/nvme_tcp_end_to_end_rhel : Step 6 - NOTICE - Reboot required if multipath was just enabled] ******************************
ok: [localhost] => {
    "msg": "NVMe native multipath was enabled via grubby and initramfs was regenerated. A REBOOT of 192.168.53.160 is required to activate multipathing. After reboot, verify with: cat /sys/module/nvme_core/parameters/multipath And verify IO policy with: cat /sys/class/nvme-subsystem/nvme-subsys*/iopolicy"
}

TASK [roles/nvme_tcp_end_to_end_rhel : Step 6 - Verify NVMe native multipath (if already enabled)] ***********************************
skipping: [localhost]

TASK [roles/nvme_tcp_end_to_end_rhel : Step 6 - Verify IO policy for NVMe subsystems (if multipath already active)] ******************
skipping: [localhost]

TASK [roles/nvme_tcp_end_to_end_rhel : Step 6 - Display IO policy] *******************************************************************
skipping: [localhost]

TASK [roles/nvme_tcp_end_to_end_rhel : Step 6 - Final NVMe namespace and subsystem verification] *************************************
skipping: [localhost]

TASK [roles/nvme_tcp_end_to_end_rhel : Step 6 - Display final NVMe namespace list] ***************************************************
skipping: [localhost]

TASK [roles/nvme_tcp_end_to_end_rhel : Step 6 - Final NVMe subsystem path verification] **********************************************
skipping: [localhost]

TASK [roles/nvme_tcp_end_to_end_rhel : Step 6 - Display final subsystem paths (multipath verification)] ******************************
skipping: [localhost]

PLAY RECAP ***************************************************************************************************************************
localhost                  : ok=53   changed=10   unreachable=0    failed=0    skipped=8    rescued=0    ignored=0