# EX260 Mock Exams

Practice under exam conditions. The real EX260 is a 3-hour, performance-based exam with no multiple-choice questions, so these mocks are task-based. A short knowledge check is included for recall, not as exam simulation.

## How to Use These Mocks

1. Build a clean lab snapshot before each mock (3 MONs + 3 OSDs minimum; 6 OSDs for erasure coding).
2. Set a timer. Do not look at the answer key until time is up.
3. Score with the rubric at the end.
4. Repeat any mock scoring below 70%.
5. After each attempt, rebuild from scratch at least once. Speed comes from repetition.

Legend:
- `MON1`, `MON2`, `MON3` = monitor hosts
- `OSD1`-`OSD3` = OSD hosts
- `CLIENT1` = client host
- `RGW1` = RADOS gateway host (can be one of the MON hosts in a small lab)
- Adapt hostnames, devices, and IPs to your lab

> These mocks are original practice material, not actual exam content. Red Hat does not endorse them.

---

## Mock Exam 1 - Deploy, Pools, Auth, CRUSH

**Time:** 90 minutes  
**Points:** 100  
**Pass:** 70

### Tasks

1. **(15 pts)** Bootstrap a containerized Ceph cluster on `MON1` using `cephadm`. Use a dedicated cluster network and a public network. Add `MON2`, `MON3`, `OSD1`, `OSD2`, `OSD3`, and `CLIENT1` as hosts.
2. **(10 pts)** Add two OSDs per OSD host using `ceph-volume`/`ceph orch`. Confirm all OSDs are `up` and `in`.
3. **(10 pts)** Create a replicated pool named `rbdprod` with 64 PGs and application `rbd`. Set size 3 and min_size 2.
4. **(10 pts)** Create an erasure-coded profile named `ec42` using `k=4,m=2`, then create an erasure-coded pool named `ecpool` using that profile with 32 PGs. Upload `/etc/hosts` as an object named `hosts-ec` into `ecpool`.
5. **(10 pts)** Create a namespace named `archive` inside `rbdprod` and store an object `testobj` in that namespace.
6. **(15 pts)** Create a CephX user `client.app` that can read and write only the `rbdprod` pool and can read the `archive` namespace. It must not have admin access.
7. **(10 pts)** Configure PG autoscaling so `rbdprod` uses `on` and `ecpool` uses `warn`.
8. **(10 pts)** Create a CRUSH bucket hierarchy `datacenter -> rack -> host` and a replicated rule named `ssdrule` that uses it. Verify the rule compiles.
9. **(10 pts)** Set the `nearfull` ratio to `0.80` and `full` ratio to `0.90` cluster-wide using the OSD map commands. Confirm the values.

### Validation Commands

```bash
ceph -s
ceph orch host ls
ceph osd tree
ceph osd pool ls detail
ceph osd pool get rbdprod size
ceph osd pool get rbdprod min_size
ceph osd erasure-code-profile get ec42
rados -p ecpool ls
rados -p rbdprod -N archive ls
ceph auth get client.app
ceph osd pool get rbdprod pg_autoscale_mode
ceph osd crush rule dump ssdrule
ceph osd dump | grep -E 'nearfull_ratio|full_ratio'
```

### Scoring Guide

| Task | Full credit | Partial credit |
|------|-------------|----------------|
| 1 | Cluster healthy; all hosts added; networks set | Cluster up but host/network missing |
| 2 | All OSDs up/in and persistent | OSDs added but not persistent |
| 3 | Pool exists with correct PG/size/min_size/app | One value wrong |
| 4 | Profile and EC pool correct; object readable | Pool created, profile wrong |
| 5 | Object exists in namespace | Namespace created but object missing |
| 6 | Caps limited correctly; no admin | Overly broad caps |
| 7 | Both modes correct | One mode correct |
| 8 | Rule compiles and uses hierarchy | Hierarchy created but rule fails |
| 9 | Both ratios set and persist | Runtime only |

---

## Mock Exam 2 - RBD, RADOSGW, CephFS

**Time:** 90 minutes  
**Points:** 100  
**Pass:** 70

### Tasks

1. **(15 pts)** In `rbdprod`, create a 10G image `webdisk`. Map it on `CLIENT1`, format it with XFS, mount it at `/mnt/web`, write `/mnt/web/data.txt`, then unmount and unmap.
2. **(10 pts)** Create a snapshot `snap-base` of `webdisk`. Clone it to `webclone` and flatten the clone. Confirm the clone is independent.
3. **(10 pts)** Export `webdisk` to `/backup/webdisk.img`. Create a new image `webimport` and import the file. Verify the content.
4. **(10 pts)** Enable one-way RBD mirroring in image mode for `webdisk` to a second cluster if available. If only one cluster is available, configure and document the required commands and check `rbd mirror image status` output.
5. **(15 pts)** Deploy a RADOS gateway on `RGW1`. Create an S3 user `s3user` with access and secret keys. Create bucket `mockbucket` and upload `/etc/hosts` as `hosts.txt`.
6. **(10 pts)** Create a Swift user `swiftuser` and upload an object to container `swiftcont` using Swift commands.
7. **(15 pts)** Create a CephFS named `cephfs1` with metadata pool `cephfs1_meta` and data pool `cephfs1_data`. Mount it persistently on `CLIENT1` at `/mnt/cephfs` using the kernel client.
8. **(10 pts)** Set a quota of 5G on `/mnt/cephfs/projects` using CephFS extended attributes. Create a CephFS snapshot of `/mnt/cephfs/projects` named `proj-snap` using the `.snap` directory.
9. **(5 pts)** Confirm the gateway is configured for TLS. Document the certificate paths and the `rgw_frontends` setting.

### Validation Commands

```bash
rbd info rbdprod/webdisk
rbd snap ls rbdprod/webdisk
rbd info rbdprod/webclone
rbd export rbdprod/webdisk /backup/webdisk.img
rbd import /backup/webdisk.img rbdprod/webimport
radosgw-admin user info --uid=s3user
aws --endpoint-url http://RGW1:8080 s3 ls s3://mockbucket
swift -A http://RGW1:8080/auth -U swiftuser -K <key> list swiftcont
ceph fs status cephfs1
getfattr -n ceph.quota.max_bytes /mnt/cephfs/projects
ls /mnt/cephfs/projects/.snap
mount | grep ceph
ceph config get client rgw_frontends
```

### Scoring Guide

- Full credit only if the task works after a reboot.
- Persistent mounts require `/etc/fstab` or a systemd unit.
- S3/Swift tasks require a successful upload and download, not just user creation.

---

## Mock Exam 3 - Full EX260 Simulation

**Time:** 180 minutes  
**Points:** 300  
**Pass:** 210

Complete all tasks. The point values approximate exam weighting. Any configuration that does not survive a reboot loses full credit.

### Section A - Installation and Configuration (60 pts)

1. **(20)** Install a containerized Ceph cluster with 3 MONs, 3 MGRs, and at least 6 OSDs across 3 hosts. Set public and cluster networks.
2. **(10)** Add a new MON host and a new OSD host to the running cluster.
3. **(10)** Change the default `osd_pool_default_size` to 3 and `osd_pool_default_min_size` to 2 persistently.
4. **(10)** Create a client user `client.ro` with read-only access to `rbdprod` and no access to other pools.
5. **(10)** Configure PG autoscaling `on` for all new pools.

### Section B - Pools, Namespaces, Erasure Coding (40 pts)

6. **(10)** Create `pool-a` replicated (size 3, 64 PGs) and `pool-b` erasure-coded with `k=4,m=2`.
7. **(10)** Create namespace `ns1` in `pool-a` and put `file1` in it.
8. **(10)** Upload a 20 MB file to `pool-b` and verify its checksum after download.
9. **(10)** Create a CRUSH rule that pins `pool-b` to a specific host set, then remap all PGs in `pool-b` and confirm redistribution.

### Section C - Block Storage (60 pts)

10. **(15)** Create a 20G RBD image, map, format XFS, mount persistently, and store data.
11. **(10)** Snapshot the image, clone it, and flatten the clone.
12. **(10)** Export the image to a file, create an incremental export after new writes, and import both correctly into a new image.
13. **(15)** Configure one-way RBD mirroring (pool mode or image mode), deploy the mirror agent, and show `up+replaying` status.
14. **(10)** Tune RBD client access (queue depth and related settings) and document the effect.

### Section D - Object Storage (50 pts)

15. **(15)** Deploy RGW, create an S3 user, create a bucket, and upload/download an object with the AWS CLI.
16. **(10)** Deploy a multisite RGW configuration (or document the exact steps and config if only one site is available).
17. **(10)** Create a Swift user and perform upload/list/download.
18. **(10)** Export an S3 bucket through NFS and mount it on a client.
19. **(5)** Enable in-transit encryption for RGW and confirm HTTPS access.

### Section E - File Storage (40 pts)

20. **(15)** Create CephFS and mount it persistently on two clients.
21. **(10)** Configure a directory quota and verify it is enforced.
22. **(10)** Create and restore a CephFS snapshot.
23. **(5)** Confirm the MDS is active and standby is available.

### Section F - Operations, Tuning, Troubleshooting (50 pts)

24. **(10)** Mark an OSD `out`, observe recovery, then mark it `in` and confirm health returns to `HEALTH_OK`.
25. **(10)** Pause and resume scrubbing; set `nodeep-scrub` and later clear it.
26. **(10)** Throttle recovery/rebalancing and then restore defaults.
27. **(10)** Troubleshoot a deliberately broken client mount or RGW endpoint and document the fix.
28. **(10)** Integrate Ceph with OpenStack Glance and Cinder (or document the exact config changes and validate with `openstack image create` / `openstack volume create` if available).

### Validation

```bash
ceph -s
ceph health detail
ceph orch ps
ceph osd tree
ceph osd pool ls detail
ceph df detail
rbd info pool-a/webdisk
rbd mirror pool status
radosgw-admin sync status
ceph fs status
ceph pg dump_stuck
systemctl status ceph.target
mount | grep -E 'rbd|ceph'
```

### Scoring Guide

- Subtract 50% for any task that works only until reboot.
- Subtract full points for wrong names, sizes, or paths even if the technology works.
- A cluster in `HEALTH_ERR` at the end costs 20 points.
- If time runs out, list completed vs incomplete tasks and score only completed work.

---

## Mock Exam 4 - Troubleshooting and Tuning

**Time:** 60 minutes  
**Points:** 100  
**Pass:** 70

Your instructor/lab partner breaks the cluster. Diagnose and fix each issue.

### Scenarios

1. **(20 pts)** One OSD is `down`. Determine whether it is a disk, service, or network issue, and restore it without data loss.
2. **(20 pts)** Clients cannot mount CephFS. `ceph fs status` shows no active MDS. Restore service.
3. **(15 pts)** An S3 request returns `403 AccessDenied`. Diagnose the RGW user/caps and fix it.
4. **(15 pts)** The cluster is stuck in `HEALTH_WARN` with `pgs stale`. Identify the cause and recover.
5. **(15 pts)** Recovery is saturating the network. Throttle it, then restore defaults after recovery.
6. **(15 pts)** A MON is unreachable but the quorum still holds. Rejoin or replace the MON safely.

### Diagnostic Starting Points

```bash
ceph -s
ceph health detail
ceph orch ps
ceph osd tree
ceph osd metadata <id>
journalctl -u <service> --no-pager -n 100
ceph pg dump_stuck
ceph fs status
ceph fs dump
radosgw-admin user info --uid=<uid>
ceph config dump
ceph mon stat
```

### Scoring Guide

- Full credit for root cause + permanent fix + verification.
- Partial credit for a workaround that does not persist.
- Zero if the fix causes data loss or takes down quorum.

---

## Rapid Knowledge Check

Answer without looking anything up. 25 questions, 4 points each (100 total). Answers are below.

1. What does RADOS stand for, and what role does it play in Ceph?
2. Which daemon stores data as objects on disks?
3. Which daemon maintains the cluster map and quorum?
4. What is a placement group (PG)?
5. What does CRUSH compute, and what inputs does it use?
6. What is the difference between replication and erasure coding?
7. In a `k=4,m=2` erasure-coded pool, how many OSDs can fail without data loss?
8. What command shows overall cluster health?
9. What does `ceph osd tree` show?
10. What is the difference between `ceph osd out` and `ceph osd down`?
11. What is the purpose of a CephX keyring?
12. Which command creates a restricted CephX user?
13. What is the difference between RBD, CephFS, and RGW?
14. Which command creates an RBD snapshot?
15. What does `rbd flatten` do to a clone?
16. What is RBD mirroring used for?
17. What are the two common RGW APIs?
18. Which command creates a RADOS gateway user?
19. What is a CephFS metadata pool used for?
20. How are CephFS directory quotas configured and inspected?
21. What is the difference between scrub and deep-scrub?
22. Which settings control OSD fullness thresholds?
23. What does PG autoscaling do?
24. Why must configurations persist after reboot in EX260?
25. What are the recommended prerequisites and training course for EX260?

### Answer Key

1. Reliable Autonomic Distributed Object Store; the foundation layer that stores all data as objects.
2. OSD (Object Storage Daemon).
3. MON (Monitor).
4. A logical grouping of objects used for placement and replication; the unit CRUSH maps to OSDs.
5. It maps objects/PGs to OSDs using the cluster map, CRUSH rule, and a hash of the object/PG ID.
6. Replication stores full copies; erasure coding stores fragments plus parity and uses less space at the cost of CPU and recovery complexity.
7. Two (`m=2`).
8. `ceph -s` (or `ceph status`).
9. The OSD hierarchy, weights, and up/in state.
10. `out` removes an OSD from data placement (triggers rebalance); `down` means the daemon is not responding.
11. It stores the user's secret key used to authenticate to Ceph services.
12. `ceph auth get-or-create client.<name> mon '...' osd '...'` (with restricted caps).
13. RBD = block device, CephFS = POSIX file system, RGW = S3/Swift object storage.
14. `rbd snap create <pool>/<image>@<snap>`.
15. It copies the parent data into the clone so the clone no longer depends on the parent.
16. Asynchronous replication of RBD images to a remote cluster for disaster recovery.
17. Amazon S3 and OpenStack Swift.
18. `radosgw-admin user create --uid=<uid> --display-name=<name>`.
19. It stores CephFS metadata (directory hierarchy, inodes, journal).
20. With the `ceph.quota.max_bytes` and `ceph.quota.max_files` extended attributes, set via `setfattr` and read via `getfattr`.
21. Scrub checks metadata and checksums; deep-scrub reads and verifies all data blocks.
22. `nearfull_ratio`, `backfillfull_ratio`, and `full_ratio` (also `mon_osd_full_ratio` variants depending on version).
23. It automatically adjusts the number of PGs per pool based on usage and target ratios.
24. The exam grades the final state of the systems, and Red Hat performance exams require persistence after reboot.
25. RHCSA or equivalent; recommended course CL260 - Cloud Storage with Red Hat Ceph Storage.

---

## Score Sheet

| Mock | Date | Time Used | Score | Pass (Y/N) | Weak Areas |
|------|------|-----------|-------|------------|------------|
| Mock 1 - Deploy/Configure | | | /100 | | |
| Mock 2 - Storage Services | | | /100 | | |
| Mock 3 - Full Simulation | | | /300 | | |
| Mock 4 - Troubleshooting | | | /100 | | |
| Rapid Knowledge Check | | | /100 | | |

### Readiness Rule of Thumb
- Below 70%: review notes and repeat the matching labs.
- 70-84%: repeat the mock and focus on speed and persistence.
- 85%+ on Mock 3 twice: book EX260.

## After Each Mock
- [ ] Reboot all nodes and re-verify every task
- [ ] Record exact commands that failed
- [ ] Update [progress/PROGRESS_TRACKER.md](../progress/PROGRESS_TRACKER.md)
- [ ] Add missing commands to [resources/QUICK_CHEATSHEET.md](../resources/QUICK_CHEATSHEET.md)
