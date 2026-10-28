# 01 - Ceph Architecture Deep Dive

## RADOS Layer
RADOS is the heart of Ceph. All interfaces (RBD, CephFS, RGW) sit on top of librados.

**Key properties**:
- Strong consistency
- Self-managing, self-healing
- Intelligent storage nodes (OSDs) do work (replication, recovery, rebalance)
- Data placement via CRUSH, not central lookup tables

## Daemons

### MON (Monitor)
- Maintain cluster map (monmap, osdmap, pgmap, crushmap, mdsmap)
- Paxos consensus for map changes
- Authentication/authorization
- Typically odd number (3,5) for quorum
- Don't store data, store maps/state

### OSD (Object Storage Daemon)
- One per disk/storage device typically
- Stores objects on physical disk (BlueStore recommended)
- Handles replication, recovery, scrubbing
- Reports to MON, heartbeats to peers
- Peering and data integrity

### MGR (Manager)
- Collects metrics/stats
- Provides REST API, dashboard
- Modules (prometheus, influx, balancer, etc.)
- Active/standby for HA

### MDS (Metadata Server)
- Only for CephFS
- Manages file metadata (inodes, directories)
- Caches metadata for performance
- Active/standby or multiple active (mds_rank)

### RGW (RADOS Gateway)
- Object storage service
- S3 and Swift APIs
- Can use CivetWeb or Nginx/HAProxy
- Uses RADOS pools (data, index, meta)

## CRUSH & Placement
**CRUSH** computes where data goes without needing a central directory.

Key concepts:
- **CRUSH rule**: Defines placement policy (replicated vs EC, failure domains)
- **Failure domain**: host, rack, row, datacenter (isolate failures)
- **Bucket types**: root, room, datacenter, rack, host, osd
- **Weight**: Based on device capacity
- **Placement**: `CRUSH(pg_id, pool) -> list of OSDs`

## Placement Groups (PGs)
- Groups objects to reduce mapping table size
- Each PG maps to a set of OSDs per CRUSH rule
- More PGs = better distribution but more memory/CPU
- `pg_num`, `pgp_num` are key tuning parameters
- States: active, clean, peering, degraded, recovering, undersized, etc.

## BlueStore vs FileStore (Historical)
- **BlueStore** (current default): Direct to block device, no filesystem overhead, checksums, better performance
- **FileStore** (legacy): Uses XFS/ext4, write-ahead journal

## Cluster Maps
- `monmap`, `osdmap`, `pgmap`, `crushmap`, `mdsmap`, `fsmap`

## Learning Exercises
- [ ] Trace how a write flows from client to OSDs
- [ ] Explain CRUSH vs consistent hashing
- [ ] Understand PG states and why they matter
- [ ] Know when MDS is needed
