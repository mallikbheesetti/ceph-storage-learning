# Red Hat Ceph Certification Path

This program is aligned to the official Red Hat Ceph Storage certification path. Use it to move from Ceph fundamentals to a Red Hat Certified Specialist credential, and optionally toward Red Hat Certified Architect (RHCA).

## Target Credential

| Item | Detail |
|------|--------|
| Certification | Red Hat Certified Specialist in Ceph Cloud Storage |
| Exam | **EX260** |
| Format | Performance-based, hands-on, single section |
| Duration | 3 hours |
| Scoring | Scaled 0-300. Red Hat performance exams typically require **210/300 (~70%)** |
| Validity | 3 years (Red Hat certification policy) |
| Prerequisite | RHCSA (EX200) or equivalent experience; RHCE is a plus |
| Recommended training | **CL260** - Cloud Storage with Red Hat Ceph Storage (5 days) |
| RHCA credit | Counts as one of three specialist exams toward Red Hat Certified Architect (RHCE required) |
| Official exam page | https://www.redhat.com/en/services/training/ex260-red-hat-certified-specialist-in-ceph-cloud-storage-exam |
| Official certification page | https://www.redhat.com/en/services/certification/rhcs-ceph-cloud-storage |

> Exam fees, versions, objectives, and policies change. Always confirm on the official Red Hat pages before booking.

## Certification Path

```
Linux foundation
      |
      v
RHCSA (EX200)  ------------ required knowledge base
      |
      v
Recommended course: CL260 - Cloud Storage with Red Hat Ceph Storage
      |
      v
EX260 - Red Hat Certified Specialist in Ceph Cloud Storage
      |
      +--> Standalone specialist credential (valid 3 years)
      |
      +--> One of 3 specialist exams toward RHCA (with RHCE)
```

### Step 1 - Build the foundation
- Linux administration: storage, LVM, filesystems, networking, firewalld, SELinux, systemd
- Containers and Podman basics (Red Hat Ceph Storage is deployed containerized)
- Ansible basics (the Red Hat installer uses Ansible playbooks)
- Optional but recommended: earn **RHCSA (EX200)**

### Step 2 - Complete aligned training
- Recommended: **CL260 - Cloud Storage with Red Hat Ceph Storage**
- Free alternative: this repo plus the upstream Ceph documentation
- Build a multi-node lab (see [lab-prep/LAB_SETUP.md](../lab-prep/LAB_SETUP.md))

### Step 3 - Pass EX260
- Practice every objective as a hands-on task, not just reading
- Anything you configure must survive a reboot
- Time yourself: the exam is 3 hours and has no multiple-choice questions

### Step 4 - Continue to RHCA (optional)
- Hold a current RHCE in the relevant specialization (earned through the Administrator + Advanced Administrator path)
- Pass EX260 plus two other specialist exams in the same concentration
- Example Enterprise Linux combination: EX260 (Ceph), EX210 (Cloud Infrastructure), EX436 (High Availability Clustering)
- RHCA is awarded automatically once the RHCE and three specialist credentials are current

## EX260 Exam Objectives Mapped to This Repo

| # | Official objective area | Study here | Primary labs |
|---|-------------------------|------------|--------------|
| 1 | Install Red Hat Ceph Storage server (containerized; Ansible installer) | [notes/01-architecture.md](../notes/01-architecture.md), [lab-prep/LAB_SETUP.md](../lab-prep/LAB_SETUP.md) | Lab 1 |
| 2 | Work with existing clusters (change config, add MON/OSD) | [notes/03-configuration.md](../notes/03-configuration.md), [notes/04-administration.md](../notes/04-administration.md) | Labs 5, 7 |
| 3 | Configure server (replicated/EC pools, namespaces, auth, ceph-volume, PG autoscale) | [notes/02-usage.md](../notes/02-usage.md), [notes/04-administration.md](../notes/04-administration.md) | Labs 5, 6, 8 |
| 4 | Provide block storage with RBD (images, snapshots, clones, mirroring, import/export) | [notes/02-usage.md](../notes/02-usage.md) | Lab 2, 10 |
| 5 | Provide object storage with RADOSGW (S3, Swift, multisite, NFS export, TLS) | [notes/02-usage.md](../notes/02-usage.md), [notes/06-security.md](../notes/06-security.md) | Lab 4, 9 |
| 6 | Provide file storage with CephFS (create, persistent mount, quotas, snapshots) | [notes/02-usage.md](../notes/02-usage.md) | Lab 3 |
| 7 | Configure a CRUSH map (bucket hierarchy, PG remap/redistribution) | [notes/04-administration.md](../notes/04-administration.md) | Lab 8 |
| 8 | Manage and update cluster maps (MON/OSD maps, OSD limits) | [notes/04-administration.md](../notes/04-administration.md) | Labs 1, 7 |
| 9 | Manage a cluster (status, OSD/MON troubleshooting) | [notes/04-administration.md](../notes/04-administration.md), [lab-prep/TROUBLESHOOTING.md](../lab-prep/TROUBLESHOOTING.md) | Labs 1, 8 |
| 10 | Tune Ceph (network, scrubbing, recovery/rebalance, RAM vs I/O) | [notes/05-maintenance-management.md](../notes/05-maintenance-management.md) | Labs 7, 8 |
| 11 | Troubleshoot server/client (RGW debug, RBD tuning) | [lab-prep/TROUBLESHOOTING.md](../lab-prep/TROUBLESHOOTING.md) | Labs 8, 9 |
| 12 | Integrate with OpenStack (Glance and Cinder) | This file, Red Hat docs | Extension lab |

## Full Objective Checklist

### 1. Install Red Hat Ceph Storage server
- [ ] Install a containerized Ceph cluster on physical or virtual systems
- [ ] Modify the provided Ansible installation files
- [ ] Bootstrap with `cephadm` and add hosts
- [ ] Understand the difference between upstream cephadm and the Red Hat installer

### 2. Work with existing server appliances
- [ ] Change a cluster configuration value persistently
- [ ] Add monitor (MON) nodes
- [ ] Add object storage device (OSD) nodes

### 3. Configure Red Hat Ceph Storage server
- [ ] Configure a replicated storage pool
- [ ] Store objects in a pool
- [ ] Store objects in a namespace within a pool
- [ ] Create and configure erasure-coded pools
- [ ] Create an erasure-coded profile with specified parameters
- [ ] Upload a file to an erasure-coded pool
- [ ] Change default settings in the configuration files
- [ ] Manage Ceph authentication (CephX)
- [ ] Create a client with restricted read/write access to MONs, OSDs, pools, and namespaces
- [ ] Manage OSDs with `ceph-volume`
- [ ] Configure placement group auto-scaling

### 4. Provide block storage with RBD
- [ ] Create an RBD image
- [ ] Obtain image information
- [ ] Map an image on a server
- [ ] Use an RBD image (filesystem, mount)
- [ ] Create an RBD snapshot
- [ ] Create an RBD clone
- [ ] Configure RBD mirrors and deploy the mirror agent
- [ ] Configure one-way mirroring in pool mode
- [ ] Configure one-way mirroring in image mode
- [ ] Check mirroring status
- [ ] Export an image to a file and import it back
- [ ] Create and apply an incremental image export

### 5. Provide object storage with RADOSGW
- [ ] Deploy a RADOS gateway
- [ ] Deploy a multisite RADOS gateway
- [ ] Provide object storage through the Amazon S3 API
- [ ] Create an RGW user that uses S3 clients
- [ ] Upload and download objects with S3 commands
- [ ] Export S3 objects using NFS
- [ ] Provide object storage through Swift
- [ ] Create an RGW user that uses the Swift interface
- [ ] Upload and download objects with Swift commands
- [ ] Configure the gateway for in-transit encryption (TLS)

### 6. Provide file storage with CephFS
- [ ] Create a CephFS file system
- [ ] Mount CephFS persistently on a client
- [ ] Configure CephFS quotas
- [ ] Create a CephFS snapshot

### 7. Configure a CRUSH map
- [ ] Create a bucket hierarchy usable by an erasure profile or replicated rule
- [ ] Remap a PG
- [ ] Remap all PGs in a pool for optimal redistribution

### 8. Manage and update cluster maps
- [ ] Manage MON and OSD maps
- [ ] Monitor and change OSD storage limits (`full`, `backfillfull`, `nearfull`)

### 9. Manage a Red Hat Ceph Storage cluster
- [ ] Determine general cluster status
- [ ] Troubleshoot OSD problems
- [ ] Troubleshoot MON problems

### 10. Tune Red Hat Ceph Storage
- [ ] Specify and tune key network parameters
- [ ] Control scrubbing and deep scrubbing
- [ ] Control recovery and rebalancing
- [ ] Control RAM utilization against I/O performance

### 11. Troubleshoot server problems
- [ ] Troubleshoot client issues
- [ ] Enable RADOS gateway debugging
- [ ] Optimize RBD client access with tuning parameters

### 12. Integrate with Red Hat OpenStack Platform
- [ ] Integrate Ceph with Glance
- [ ] Modify Glance configuration to use Ceph as the image backend
- [ ] Integrate Ceph with Cinder
- [ ] Modify Cinder configuration to use Ceph RBD volumes

## Exam-Day Checklist
- [ ] Every configuration persists after reboot
- [ ] Use `systemctl enable` / persistent config, not only runtime settings
- [ ] Verify with commands, not assumptions (`ceph -s`, `rbd info`, `ceph fs status`, `radosgw-admin`)
- [ ] Watch the clock: 3 hours for all tasks
- [ ] Do the easy objectives first and return to hard ones
- [ ] Re-read each task for exact pool names, sizes, paths, and users
- [ ] Check cluster health before finishing

## Mock Exams
See [MOCK_EXAMS.md](MOCK_EXAMS.md) for timed practical exams, a rapid knowledge check, answer keys, and a scoring sheet.

## Official Links
- EX260 exam: https://www.redhat.com/en/services/training/ex260-red-hat-certified-specialist-in-ceph-cloud-storage-exam
- Certification page: https://www.redhat.com/en/services/certification/rhcs-ceph-cloud-storage
- CL260 course (Red Hat catalog search): https://catalog.redhat.com/search?searchType=learning&q=CL260
- Red Hat Ceph Storage docs: https://access.redhat.com/documentation/en-us/red_hat_ceph_storage
- Red Hat training policies: https://www.redhat.com/en/about/red-hat-training-policies
- Certification renewal: https://www.redhat.com/en/services/certification/renewal
- RHCA - Enterprise Linux: https://www.redhat.com/en/services/certification/red-hat-certified-architect-in-enterprise-linux
