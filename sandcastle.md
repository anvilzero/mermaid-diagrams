```mermaid
flowchart LR
    
    subgraph PROXMOX [fa:fa-server Proxmox - Chester]
        direction LR
        WAN_BRIDGE
        LAN_BRIDGE
        subgraph HARDWARE
            SSD_1[fa:fa-hdd SSD 1] ---|"ZFS Mirror
            2TB"| SSD_2[fa:fa-hdd SSD 2]
            HDD_1[fa:fa-hdd HDD 1] ---|"ZFS Mirror
                8TB"| HDD_2[fa:fa-hdd HDD 2]
            PROXMOX_CPU[fa:fa-microchip 4x CPU]
            PROXMOX_RAM[fa:fa-memory 32GB RAM]
            ETH1[fa:fa-ethernet ETH1]
            ETH2[fa:fa-ethernet ETH2]
        end
        PROXMOX_CONSOLE[fa:fa-server Proxmox Console] --- LAN_BRIDGE
        subgraph VMs [Virtual Machines]
            subgraph OPNsense [opnsense]
                OPNsense_WAN
                WAN_BRIDGE
                OPNsense_LAN
            end
        end
        subgraph LXC_CONTAINERS[LXC Containers]
            NGINX_PROXY_MANAGER[NGINX Proxy Manager]
            OMADA_SDN[Omada SDN Controller]
        end
        WAN_BRIDGE --- OPNsense_WAN
        LAN_BRIDGE --- OPNsense_LAN
    end

    subgraph LOGICAL_VIEW [fa:fa-stream Logical View]
        CPU["fa:fa-microchip 6C/12T CPU
            AMD Ryzen 5 5500U"]
        RAM["fa:fa-memory 32GB RAM
            2x 16GB DDR4 SODIMM
            MAX: 64GB"]
        SSD_POOL["fa:fa-shield-alt 2TB SSD Pool
            2x M.2 2280 NVMe"]
        HDD_POOL["fa:fa-hdd 8TB HDD Pool
            2x 8TB 3.5in SATA"]
        NET[fa:fa-network-wired 2x 2.5Gbe Network]
    end

```
