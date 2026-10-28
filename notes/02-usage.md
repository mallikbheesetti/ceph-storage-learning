# 02 - Basic Usage

## Prerequisites
Assume a running cluster accessible via `ceph` CLI with proper keyring.

## RBD (Block Storage)

### Create pool and enable RBD
```bash
ceph osd pool create rbd-pool 64 64
rbd pool init rbd-pool
```

### Create and use block image
```bash
rbd create --size 10G rbd-pool/myimage
rbd list rbd-pool
rbd info rbd-pool/myimage
rbd map rbd-pool/myimage  # maps to /dev/rbdX
mkfs.ext4 /dev/rbd0
mount /dev/rbd0 /mnt
```

### Snapshots & clones
```bash
rbd snap create rbd-pool/myimage@snap1
rbd snap list rbd-pool/myimage
rbd clone rbd-pool/myimage@snap1 rbd-pool/clone1
rbd flatten rbd-pool/clone1  # make independent
```

### Resize
```bash
rbd resize --size 20G rbd-pool/myimage
```

## CephFS (File Storage)

### Create pools for CephFS
```bash
ceph osd pool create cephfs_data 64
ceph osd pool create cephfs_metadata 32
ceph fs new myfs cephfs_metadata cephfs_data
```

### Mount CephFS
**Kernel mount:**
```bash
mount -t ceph <mon1>:6789,<mon2>:6789:/ /mnt/cephfs -o name=admin,secretfile=/etc/ceph/admin.secret
```

**FUSE mount:**
```bash
ceph-fuse -m <mon1>:6789 /mnt/cephfs
```

### Basic operations
```bash
ceph fs status
ceph fs dump
ceph mds stat
```

## RGW (Object Storage)

### Create RGW user
```bash
radosgw-admin user create --uid=testuser --display-name="Test User" --email=test@example.com
# Save access_key and secret_key
```

### Create bucket and upload (S3 with AWS CLI)
```bash
aws s3 mb s3://mybucket --endpoint-url http://<rgw-host>:7480
aws s3 cp file.txt s3://mybucket/ --endpoint-url http://<rgw-host>:7480
aws s3 ls s3://mybucket/ --endpoint-url http://<rgw-host>:7480
```

### With Swift
```bash
swift -A http://<rgw-host>:7480/auth/1.0 -U testuser:swift -K <secret> list
```

## Essential CLI
```bash
ceph df                        # usage
rados df                       # pool usage details
ceph osd pool ls detail        # pool info
ceph auth list                 # users/keys
```

## Hands-on Exercises
- [ ] Create RBD, format, mount, write data
- [ ] Create snapshot and clone, test
- [ ] Setup CephFS (if MDS available) and mount
- [ ] Create RGW user, bucket, upload via S3 API
- [ ] Practice with all three interfaces
