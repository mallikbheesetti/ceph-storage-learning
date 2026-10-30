# Ceph Storage Learning Plan - EX260 Certification Track

## Overview
This plan takes you from complete beginner to ready for the **Red Hat Certified Specialist in Ceph Cloud Storage (EX260)** exam. It follows the official exam objective areas and adds hands-on labs, mock exams, and a final readiness gate.

Full certification requirements: [certification/CERTIFICATION_PATH.md](../certification/CERTIFICATION_PATH.md)

## Target Certification

| Item | Detail |
|------|--------|
| Exam | EX260 - Red Hat Certified Specialist in Ceph Cloud Storage |
| Format | Performance-based, hands-on, single section |
| Duration | 3 hours |
| Passing | Scaled 0-300; aim for 210+ (~70%) |
| Prerequisite | RHCSA or equivalent experience |
| Recommended course | CL260 - Cloud Storage with Red Hat Ceph Storage |
| RHCA credit | Yes, one of three specialist exams (requires RHCE) |

## Prerequisites
- Linux fundamentals (CLI, networking, filesystems, packages, SELinux, firewalld)
- Basic storage concepts (block/object/file, RAID, snapshots)
- Networking basics (TCP/IP, DNS, firewalls)
- Virtualization (KVM/VirtualBox/VMware) or container runtime
- Container and Ansible basics are helpful (Red Hat deployment is containerized and Ansible-driven)

## Timeline (Flexible - 10-12 weeks suggested)

### Week 1: Foundations & Architecture
**EX260 domain:** Architecture foundation for all domains

- [ ] **Day 1-2**: Distributed storage intro (CAP theorem, scaling, replication vs erasure coding)
- [ ] **Day 3-4**: Ceph history, components, use cases
- [ ] **Day 5-6**: Core architecture (MON, OSD, MDS, MGR, RGW)
- [ ] **Day 7**: Review + knowledge check

**Resources**: [notes/00-basics.md](00-basics.md), [notes/01-architecture.md](01-architecture.md), Ceph docs intro

### Week 2: Install and Deploy
**EX260 domain:** Install Red Hat Ceph Storage server

- [ ] Containerized deployment concepts (cephadm and the Red Hat Ansible installer)
- [ ] Bootstrap a cluster, add hosts, add MONs and OSDs
- [ ] Change cluster configuration persistently
- [ ] **Lab**: Deploy a 3-node cluster from scratch

**Resources**: [lab-prep/LAB_SETUP.md](../lab-prep/LAB_SETUP.md), [notes/01-architecture.md](01-architecture.md)

### Week 3: Basic Usage & Interfaces
**EX260 domains:** RBD, RADOSGW, CephFS

- [ ] **RBD (Block)**: Create pools, images, map, use with filesystem/VM
- [ ] **CephFS (File)**: Setup, mount, quotas, snapshots
- [ ] **RGW (Object/S3/Swift)**: Create users/buckets, S3 and Swift API basics
- [ ] **CLI tools**: `ceph`, `rados`, `rbd`, `ceph fs`, `radosgw-admin`
- [ ] **Lab**: Basic operations on all three interfaces

**Resources**: [notes/02-usage.md](02-usage.md), [lab-prep/LAB_EXERCISES.md](../lab-prep/LAB_EXERCISES.md)

### Week 4: Configuration & Pools
**EX260 domain:** Configure Red Hat Ceph Storage server

- [ ] Config sources (default, mon config db, local conf, CLI/runtime)
- [ ] Key config files (`ceph.conf`, keyrings)
- [ ] Replicated pools, namespaces, erasure-coded pools and profiles
- [ ] CephX authentication and restricted clients
- [ ] OSD management with `ceph-volume`
- [ ] PG autoscaling
- [ ] **Lab**: Pools, namespaces, EC profile, restricted user

**Resources**: [notes/03-configuration.md](03-configuration.md), [notes/04-administration.md](04-administration.md)

### Week 5: Block Storage (RBD)
**EX260 domain:** Provide block storage with RBD

- [ ] Images, mapping, filesystems, snapshots, clones
- [ ] RBD mirroring (pool and image mode, mirror agent)
- [ ] Export/import, full and incremental
- [ ] RBD client tuning
- [ ] **Lab**: Full RBD lifecycle and mirroring

**Resources**: [notes/02-usage.md](02-usage.md), [Mock Exam 2](../certification/MOCK_EXAMS.md)

### Week 6: Object Storage (RADOSGW)
**EX260 domain:** Provide object storage with RADOSGW

- [ ] Deploy RGW and multisite
- [ ] S3 users, buckets, upload/download
- [ ] Swift users and containers
- [ ] NFS export of S3 objects
- [ ] In-transit encryption (TLS)
- [ ] **Lab**: S3 + Swift + TLS + NFS export

**Resources**: [notes/02-usage.md](02-usage.md), [notes/06-security.md](06-security.md)

### Week 7: File Storage (CephFS)
**EX260 domain:** Provide file storage with CephFS

- [ ] Create CephFS (metadata/data pools, MDS)
- [ ] Persistent kernel and FUSE mounts
- [ ] Quotas and snapshots
- [ ] **Lab**: Multi-client CephFS with quota and snapshot restore

**Resources**: [notes/02-usage.md](02-usage.md)

### Week 8: CRUSH, Maps, Cluster Management
**EX260 domains:** Configure a CRUSH map; Manage and update cluster maps; Manage a cluster

- [ ] CRUSH bucket hierarchy, rules, PG remapping
- [ ] MON/OSD map management and OSD fullness limits
- [ ] Cluster health, OSD/MON troubleshooting
- [ ] **Lab**: Custom CRUSH rule and controlled redistribution

**Resources**: [notes/04-administration.md](04-administration.md), [lab-prep/TROUBLESHOOTING.md](../lab-prep/TROUBLESHOOTING.md)

### Week 9: Maintenance, Tuning, Troubleshooting
**EX260 domains:** Tune Ceph; Troubleshoot server and client problems

- [ ] Add/remove OSDs, MONs, MGRs
- [ ] Balancing/reweighting
- [ ] Scrubbing, deep-scrub, repair
- [ ] Network tuning, recovery/rebalance throttling, RAM vs I/O
- [ ] RGW debugging, RBD client tuning
- [ ] **Lab**: Simulate failures and recover

**Resources**: [notes/05-maintenance-management.md](05-maintenance-management.md), [lab-prep/TROUBLESHOOTING.md](../lab-prep/TROUBLESHOOTING.md)

### Week 10: Security and OpenStack Integration
**EX260 domains:** Authentication/security; Integrate with OpenStack

- [ ] CephX in depth and least privilege
- [ ] Network security (separate public/cluster networks)
- [ ] Encryption (at-rest concepts, messenger v2, RGW TLS)
- [ ] Glance and Cinder integration
- [ ] **Lab**: Harden cluster; configure Glance/Cinder backends

**Resources**: [notes/06-security.md](06-security.md), [certification/CERTIFICATION_PATH.md](../certification/CERTIFICATION_PATH.md)

### Week 11: Mock Exams and Gap Closing
**Goal:** Score 85%+ on the full mock

- [ ] Take [Mock Exam 1](../certification/MOCK_EXAMS.md) (90 min)
- [ ] Take [Mock Exam 2](../certification/MOCK_EXAMS.md) (90 min)
- [ ] Take [Mock Exam 3 - full simulation](../certification/MOCK_EXAMS.md) (180 min)
- [ ] Take [Mock Exam 4 - troubleshooting](../certification/MOCK_EXAMS.md) (60 min)
- [ ] Review every missed task and repeat the matching lab

### Week 12: Final Readiness
- [ ] Rebuild the cluster from scratch without notes
- [ ] Repeat Mock Exam 3 twice at 85%+
- [ ] Complete the Rapid Knowledge Check at 90%+
- [ ] Confirm all items in the [EX260 objective checklist](../certification/CERTIFICATION_PATH.md)
- [ ] Book the exam

## Exam Readiness Gate
You are ready to book EX260 when all are true:
- [ ] Full mock exam scored 85%+ twice
- [ ] Cluster can be rebuilt from scratch in under 90 minutes
- [ ] All configurations survive reboot
- [ ] Every objective checklist item is completed
- [ ] Rapid Knowledge Check scored 90%+

## Learning Tips
- Do hands-on for every concept - reading alone is not enough
- Break things in the test lab and fix them
- Use official Ceph and Red Hat docs as the source of truth
- Focus on understanding PGs and CRUSH - they are key
- Practice persistence: reboot after every lab and re-verify
- Join the Ceph community (ceph.io, Slack/Matrix)
