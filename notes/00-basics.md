# 00 - Ceph Basics

## What is Ceph?
Ceph is an open-source, software-defined, distributed storage system designed for scalability, reliability, and performance. It provides unified storage: object, block, and file from a single cluster.

## Key Properties
- **Distributed**: No single point of failure (SPOF)
- **Scalable**: Petabyte+ scale, add nodes linearly
- **Self-healing**: Automatically recovers from failures
- **Software-defined**: Runs on commodity hardware
- **Unified storage**: RBD, CephFS, RGW in one platform

## Storage Interfaces
| Interface | Use Case | Protocols/Access |
|-----------|----------|-----------------|
| **RBD (RADOS Block Device)** | Virtual disks, cloud volumes (OpenStack Cinder), databases | Kernel module, `rbd` CLI, librbd |
| **CephFS** | Shared POSIX filesystem, HPC, home dirs | Kernel mount, FUSE, NFS-Ganesha |
| **RGW (RADOS Gateway)** | Object storage, backups, archives, apps | S3-compatible REST, Swift-compatible REST |

## Core Concepts
- **RADOS**: Reliable Autonomic Distributed Object Store - the foundation
- **Objects**: Basic unit of storage in RADOS
- **Pools**: Logical partitions of objects with rules (replication/EC)
- **PGs (Placement Groups)**: Aggregation of objects for placement/rebalancing
- **CRUSH**: Controlled Replication Under Scalable Hashing - data placement algorithm
- **Monitors (MON)**: Cluster map, quorum, consensus (Paxos)
- **OSDs (Object Storage Daemons)**: Store data, handle replication/recovery
- **MGR (Manager)**: Metrics, dashboards, modules, orchestration
- **MDS (Metadata Server)**: Metadata for CephFS only
- **RGW**: Object gateway daemons

## Data Protection
- **Replication**: Each object copied N times (e.g., size=3)
- **Erasure Coding (EC)**: Split object into k+m chunks, more space efficient, higher CPU

## Quick Commands
```bash
ceph -s                    # Cluster status
ceph health detail         # Detailed health
ceph osd tree              # OSD topology
ceph df                    # Storage usage
ceph mon stat              # Monitor status
```

## Learning Exercises
- [ ] Explain difference between block/object/file in your own words
- [ ] Draw Ceph architecture mentally and list components
- [ ] Compare replication vs erasure coding
- [ ] Understand when to use RBD/CephFS/RGW
