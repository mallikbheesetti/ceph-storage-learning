# 05 - Maintenance & Management

## Routine Maintenance
- **Scrubbing**: Checks object consistency (shallow/deep)
- **Balancing**: Even distribution across OSDs
- **Rebalancing**: After adding/removing OSDs
- **Upgrades**: Follow release notes, upgrade order
- **Backups**: Configs, keyrings, CRUSH maps, RGW data considerations

## Scrub Operations
```bash
ceph pg dump pgs | grep scrub
ceph osd pool set <pool> scrub_min_interval <sec>
ceph osd pool set <pool> scrub_max_interval <sec>
```

States like `scrubbing`, `deep-scrub` appear during checks.

## Adding Capacity
1. Add new OSD node/disks
2. Create OSDs
3. CRUSH updates automatically
4. Data rebalances (can be throttled)
5. Monitor recovery

Throttle if impacting prod: `osd_recovery_max_active`, `osd_max_backfills`

## Removing OSDs
```bash
ceph osd out osd.N
# wait for rebalancing
ceph osd crush remove osd.N
ceph auth del osd.N
ceph osd rm osd.N
```

## Upgrades (General)
- Check compatibility matrix
- Upgrade MONs first or follow official order
- Upgrade OSDs, MGR, MDS, RGW
- Use `ceph versions`, check health between steps
- Have rollback plan

## Monitoring
Key metrics to watch:
- Cluster health
- OSD usage % per node/disk
- PG states (degraded/undersized/recovering)
- Latency/throughput
- MON quorum
- Network errors

Tools: `ceph -s`, dashboard, Prometheus+Grafana

## Troubleshooting Common Issues
| Issue | Symptoms | Approach |
|-------|----------|----------|
| OSD down | HEALTH_WARN, pg degraded | Check logs, disk, network, bring up or replace |
| PG stuck inactive | stuck in peering | Check MON/OSD connectivity, CRUSH |
| Slow requests | high latency | Check network, slow disks, recovery/backfill |
| Full cluster | near full OSDs | Add capacity or delete data |
| Clock skew | MON issues | NTP/time sync |

## Backups & Recovery Concepts
- **RBD snapshots**: Local to cluster
- **RBD export/import**: For off-cluster copies
- **RGW**: Consider multisite or backups
- **CephFS**: Snapshots available but depends
- **Cluster config**: Backup `/etc/ceph/`, mon store if needed

```bash
rbd export rbd-pool/myimage /backup/myimage.img
rbd import /backup/myimage.img rbd-pool/myimage-restored
```

## Exercises
- [ ] Simulate OSD failure and observe recovery
- [ ] Add an OSD in lab and watch rebalance
- [ ] Safely remove an OSD
- [ ] Check stuck PGs and understand recovery
- [ ] Practice backup/restore of RBD
