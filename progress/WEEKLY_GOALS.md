# Weekly Goals - EX260 Certification Track

## Week 1: Foundations
**Focus**: Basics + Architecture
- [ ] Read 00-basics.md and 01-architecture.md
- [ ] Understand RADOS, MON/OSD/MGR/MDS/RGW
- [ ] Understand CRUSH and PGs conceptually
- [ ] Review Ceph.io beginner docs
- **Goal**: Explain Ceph architecture to someone else

## Week 2: Install and Deploy
**Focus**: EX260 installation objectives
- [ ] Review containerized deployment concepts
- [ ] Bootstrap a cluster with cephadm/installer
- [ ] Add hosts, MONs, and OSDs
- [ ] Change configuration persistently
- **Goal**: Rebuild a 3-node cluster from scratch

## Week 3: Basic Usage
**Focus**: RBD, CephFS, RGW
- [ ] Complete all 02-usage.md exercises
- [ ] Create and use RBD
- [ ] Setup/mount CephFS (lab)
- [ ] Create RGW user and S3/Swift operations
- **Goal**: Comfortable with all three interfaces

## Week 4: Configuration and Pools
**Focus**: Config system, pools, auth
- [ ] Read 03-configuration.md
- [ ] Practice ceph config commands
- [ ] Create replicated and EC pools and namespaces
- [ ] Create restricted CephX users
- [ ] Configure PG autoscaling
- **Goal**: Know how to configure a cluster to spec

## Week 5: Block Storage
**Focus**: RBD objectives
- [ ] Complete RBD lifecycle: create, map, mount, snapshot, clone
- [ ] Configure RBD mirroring (pool and image mode)
- [ ] Export/import full and incremental
- [ ] Practice RBD client tuning
- **Goal**: Complete Mock Exam 2 RBD section at full marks

## Week 6: Object Storage
**Focus**: RADOSGW objectives
- [ ] Deploy RGW and create S3/Swift users
- [ ] Upload/download with S3 and Swift
- [ ] Configure NFS export of S3 objects
- [ ] Enable in-transit encryption
- **Goal**: Working S3 and Swift endpoint with TLS

## Week 7: File Storage
**Focus**: CephFS objectives
- [ ] Create CephFS with separate metadata/data pools
- [ ] Persistent kernel and FUSE mounts
- [ ] Configure quotas and snapshots
- **Goal**: Multi-client CephFS with enforced quota

## Week 8: CRUSH and Cluster Maps
**Focus**: CRUSH, MON/OSD maps
- [ ] Build a bucket hierarchy and rule
- [ ] Remap PGs and observe redistribution
- [ ] Manage OSD fullness limits
- [ ] Troubleshoot OSD/MON issues
- **Goal**: Explain and modify CRUSH placement confidently

## Week 9: Maintenance and Tuning
**Focus**: Operations, tuning, troubleshooting
- [ ] Practice OSD add/remove and failure recovery
- [ ] Control scrub, deep-scrub, recovery, rebalance
- [ ] Tune network and RAM vs I/O
- [ ] Enable RGW debugging and tune RBD clients
- **Goal**: Complete Mock Exam 4 at 70+

## Week 10: Security and OpenStack
**Focus**: Hardening and integration
- [ ] Read 06-security.md
- [ ] Create least-privilege users and secure networks
- [ ] Configure RGW TLS
- [ ] Integrate Ceph with Glance and Cinder
- **Goal**: Pass the security and integration checklist items

## Week 11: Mock Exams
**Focus**: Timed practice
- [ ] Mock Exam 1 (90 min)
- [ ] Mock Exam 2 (90 min)
- [ ] Mock Exam 3 full simulation (180 min)
- [ ] Mock Exam 4 (60 min)
- [ ] Rapid Knowledge Check
- **Goal**: 85%+ on Mock 3 and close all gaps

## Week 12: Final Readiness
**Focus**: Consolidation and booking
- [ ] Rebuild cluster from scratch without notes
- [ ] Repeat Mock Exam 3 twice at 85%+
- [ ] Review all notes and cheat sheet
- [ ] Confirm every EX260 checklist item
- [ ] Book and pass EX260
- **Goal**: Exam-ready and scheduled
