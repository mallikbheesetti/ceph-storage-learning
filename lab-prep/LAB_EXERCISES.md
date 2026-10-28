# Lab Exercises

Do these in order. Document everything you do (commands, outputs, issues).

## Lab 1: Cluster Basics
**Goal**: Verify cluster health and explore

- [ ] SSH into cluster nodes
- [ ] Run `ceph -s`, `ceph health detail`
- [ ] Check `ceph mon stat`, `ceph osd tree`
- [ ] Check `ceph df`, `rados df`
- [ ] Explore `ceph auth list`
- **Notes**: Document cluster state

## Lab 2: RBD Block Storage
**Goal**: Create and use block device

- [ ] Create pool: `ceph osd pool create lab-rbd 32 32`
- [ ] Enable: `rbd pool init lab-rbd`
- [ ] Create image: `rbd create lab-rbd/testimg --size 5G`
- [ ] Map on client: `rbd map lab-rbd/testimg`
- [ ] Format: `mkfs.xfs /dev/rbd0` (or ext4)
- [ ] Mount: `mount /dev/rbd0 /mnt/rbd-test`
- [ ] Write test file
- [ ] Unmount and unmap
- [ ] Create snapshot: `rbd snap create lab-rbd/testimg@snap1`
- [ ] Clone and flatten
- **Notes**: Document full workflow

## Lab 3: CephFS
**Goal**: Setup and use CephFS

- [ ] Create data/metadata pools
- [ ] Create FS: `ceph fs new labfs <meta-pool> <data-pool>`
- [ ] Check MDS: `ceph mds stat`
- [ ] Get client key or use admin
- [ ] Mount with kernel: `mount -t ceph ...`
- [ ] Or FUSE: `ceph-fuse`
- [ ] Create files/dirs, test permissions
- [ ] Check `ceph fs status`
- **Notes**: Troubleshoot if MDS not active

## Lab 4: RGW Object Storage
**Goal**: S3-compatible object storage

- [ ] Create RGW user with radosgw-admin
- [ ] Note access/secret keys
- [ ] Configure AWS CLI with endpoint
- [ ] Create bucket: `aws s3 mb s3://labbucket --endpoint-url ...`
- [ ] Upload/download objects
- [ ] List buckets/objects
- [ ] Test with curl if desired
- **Notes**: Try both S3 and basic operations

## Lab 5: Configuration Management
**Goal**: Work with configs

- [ ] View: `ceph config dump`
- [ ] Get/set a config: `ceph config set global log_to_file true` (test)
- [ ] View daemon config: `ceph config show osd.0`
- [ ] Check ceph.conf on nodes
- [ ] Understand precedence
- [ ] Revert change
- **Notes**: Document changes

## Lab 6: Authentication & Users
**Goal**: CephX management

- [ ] List auth: `ceph auth list`
- [ ] Create read-only user: `ceph auth get-or-create client.ro mon 'allow r' osd 'allow r'`
- [ ] Create pool-restricted user
- [ ] Test with keyring
- [ ] Delete test user
- **Notes**: Test access restrictions

## Lab 7: OSD Management
**Goal**: Add/remove/out/in

- [ ] Check OSD tree
- [ ] Mark OSD out: `ceph osd out osd.X`
- [ ] Watch rebalance: `ceph -w`
- [ ] Mark back in: `ceph osd in osd.X`
- [ ] (Advanced) Add new OSD if disk available
- [ ] (Advanced) Remove OSD safely
- **Notes**: Observe PG states

## Lab 8: PGs & Troubleshooting
**Goal**: Understand PG states

- [ ] `ceph pg stat`
- [ ] `ceph pg dump | head -30`
- [ ] Check for stuck PGs: `ceph pg dump_stuck`
- [ ] Understand degraded/peering/recovering
- [ ] Trigger recovery observation
- **Notes**: Document states you see

## Lab 9: Security Basics
**Goal**: Apply security practices

- [ ] Review keyring permissions
- [ ] Create minimal-privilege user
- [ ] Check network config (public/cluster)
- [ ] (If RGW) test TLS conceptually
- [ ] Review auth caps
- **Notes**: Create hardening checklist for your lab

## Lab 10: Backup & Restore
**Goal**: Data protection

- [ ] Create RBD with data
- [ ] Snapshot RBD
- [ ] Export: `rbd export lab-rbd/testimg /tmp/backup.img`
- [ ] Create new image and import
- [ ] Verify data
- [ ] Clean up
- **Notes**: Document backup strategy
