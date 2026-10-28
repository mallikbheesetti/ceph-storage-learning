# Lab Setup Guide

You need a safe environment to practice. **Never practice on production!**

## Options

### Option 1: Virtual Machines (Recommended for learning)
Use VirtualBox, KVM, VMware, or Proxmox.
- **Minimum**: 3 VMs (1 MON+MGR+OSD combo or separate) - 4-6GB RAM each, 2-4 CPUs
- **Better**: 4 VMs (3 MON/MGR, 1+ clients) with extra disks for OSDs
- **OS**: Ubuntu 22.04/24.04, Rocky Linux 9, or CentOS Stream (check Ceph compatibility)

### Option 2: Vagrant + VirtualBox
Automate VM creation. Good for reproducibility.

### Option 3: Containers (Kubernetes/Rook)
More advanced - better for cloud-native, but steeper for pure Ceph basics.
Recommended after understanding standalone Ceph.

### Option 4: Cephadm/Orchestrator
Modern deployment method. Good to learn.

## Hardware Requirements (Lab)
- **RAM**: 16GB+ minimum (8GB possible but tight)
- **CPU**: 4+ cores
- **Disk**: 50GB+ for VMs + space for OSD disks (can use virtual disks)
- **Network**: Bridged/NAT with host-only for cluster network

## Network Design
- **Public network**: Client access to MONs/RGWs (e.g., 192.168.100.0/24)
- **Cluster network**: OSD replication/recovery (e.g., 192.168.200.0/24) - can be same in small lab

## Lab Topology (Suggested Minimal)
```
ceph-mon1, ceph-mon2, ceph-mon3 (MON/MGR)
ceph-osd1, ceph-osd2, ceph-osd3 (OSD with extra disks)
ceph-client (for testing RBD/CephFS/RGW)
```

## Installation Approaches
1. **cephadm** (modern, containerized) - Recommended for recent Ceph versions
2. **ceph-ansible** (automation)
3. **Manual package install** (educational, see old docs)

## Quick Start Resources
- [Ceph Installation Guide](https://docs.ceph.com/en/latest/install/)
- [Cephadm](https://docs.ceph.com/en/latest/cephadm/)
- [Rook](https://rook.io/) (K8s)

## Preparation Checklist
- [ ] Choose hypervisor
- [ ] Plan VM specs and networking
- [ ] Download OS ISO
- [ ] Create VMs
- [ ] Configure SSH keys
- [ ] Update packages
- [ ] Set hostnames/hosts file
- [ ] Disable firewalls or configure rules (carefully in lab)
- [ ] Time sync (chrony/ntp)
