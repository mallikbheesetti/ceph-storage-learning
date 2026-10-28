# Ceph Storage Learning Plan

## Overview
This plan is designed for complete beginners. Focus on understanding concepts first, then hands-on practice.

## Prerequisites
- Linux fundamentals (CLI, networking, filesystems, packages)
- Basic storage concepts (block/object/file, RAID, snapshots)
- Networking basics (TCP/IP, DNS, firewalls)
- Virtualization (KVM/VirtualBox/VMware) or container runtime

## Timeline (Flexible - 8-12 weeks suggested)

### Week 1: Foundations & Architecture (Basic Usage - Part 1)
**Goal**: Understand distributed storage concepts and Ceph fundamentals

- [ ] **Day 1-2**: Distributed storage intro (CAP theorem, scaling, replication vs erasure coding)
- [ ] **Day 3-4**: Ceph history, components, use cases
- [ ] **Day 5-6**: Core architecture (MON, OSD, MDS, RGW, MGR)
- [ ] **Day 7**: Review + quiz

**Resources**: Ceph docs intro, "Beginner's Guide to Ceph" (Ceph.io)

### Week 2: Basic Usage & Interfaces
**Goal**: Learn how to interact with Ceph

- [ ] **RBD (Block)**: Create pools, images, map, use with filesystem/VM
- [ ] **CephFS (File)**: Setup, mount, permissions
- [ ] **RGW (Object/S3/Swift)**: Create users/buckets, S3 API basics
- [ ] **CLI tools**: `ceph`, `rados`, `rbd`, `ceph fs`, `radosgw-admin`
- [ ] **Lab**: Basic operations on all three interfaces

### Week 3: Configuration Fundamentals
**Goal**: Understand Ceph configuration system

- [ ] Config sources (default, mon config db, local conf, CLI/runtime)
- [ ] Key config files (`ceph.conf`, keyrings)
- [ ] Common settings (network, auth, pools)
- [ ] Tuning basics
- [ ] **Lab**: Modify configs and apply

### Week 4: Administration
**Goal**: Cluster management and day-to-day ops

- [ ] Cluster health monitoring (`ceph -s`, `ceph health detail`)
- [ ] Authentication/authorization (CephX)
- [ ] Pools, PGs (Placement Groups) - deep dive
- [ ] CRUSH maps and placement
- [ ] User/key management
- [ ] **Lab**: Administer a test cluster

### Week 5: Maintenance & Management
**Goal**: Upgrades, scaling, troubleshooting

- [ ] Adding/removing OSDs
- [ ] Adding/removing MONs/MGRs
- [ ] Balancing/reweighting
- [ ] Scrubbing, deep-scrub, repair
- [ ] Upgrades and compatibility
- [ ] Backups/snapshots/cloning
- [ ] **Lab**: Simulate failures and recovery

### Week 6-7: Security
**Goal**: Secure Ceph deployments

- [ ] Authentication (CephX) in depth
- [ ] Network security (separate public/cluster networks)
- [ ] Encryption (at-rest concepts, messenger v2)
- [ ] RGW security (ACLs, policies, TLS)
- [ ] Key management
- [ ] Hardening checklist
- [ ] **Lab**: Secure cluster components

### Week 8-12: Projects & Deep Dives
- [ ] Build multi-node test cluster (recommended)
- [ ] Disaster recovery scenario
- [ ] Performance testing basics
- [ ] Document your learnings
- [ ] Contribute notes to this repo

## Learning Tips
- Do hands-on for every concept - reading alone is not enough
- Break things in test lab and fix them
- Use official Ceph docs as source of truth
- Join Ceph community (ceph.io, Slack/Matrix)
- Focus on understanding PGs and CRUSH - they are key
