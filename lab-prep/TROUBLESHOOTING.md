# Troubleshooting Guide

## General Approach
1. Check health: `ceph -s` and `ceph health detail`
2. Look at logs: `/var/log/ceph/` or journalctl
3. Check connectivity (network, ports)
4. Check time sync
5. Understand recent changes
6. Fix in lab, document

## Common Issues

### Cluster not healthy
```bash
ceph health detail
ceph -w  # watch
journalctl -u ceph-mon@<id> -n 50
journalctl -u ceph-osd@<id> -n 50
```

### OSD down
**Symptoms**: HEALTH_WARN, osd.X down
**Checks**:
- `ceph osd tree` - see status
- `systemctl status ceph-osd@X`
- Check disk: `smartctl -a /dev/sdX`, `lsblk`
- Check network to OSD
- Check logs

**Actions**: Start if stopped, check hardware, replace disk if failed

### PGs stuck inactive/peering
```bash
ceph pg dump_stuck
ceph pg <pgid> query
```
**Causes**: MON quorum issues, OSD connectivity, CRUSH issues
**Fix**: Ensure MONs up, OSDs reachable, check network

### Slow requests
**Symptoms**: "slow ops" in health
**Checks**:
- Network latency/congestion
- Disk performance
- Recovery/backfill active
- OSD overload
**Actions**: Throttle recovery, check hardware

### Clock skew
```bash
ceph mon dump
timedatectl
chronyc tracking  # or ntpq -p
```
**Fix**: Sync time with NTP/chrony across all nodes

### Full OSDs
```bash
ceph df
ceph osd df
```
**Fix**: Add capacity, balance, or delete data. Nearfull ratios matter.

### Authentication failures
**Symptoms**: permission denied
**Checks**:
- Keyring present and correct
- `ceph auth list` - check caps
- Entity name matches
**Fix**: Add/fix auth with correct caps

### MDS issues (CephFS)
```bash
ceph mds stat
ceph fs status
```
**Fix**: Check MDS daemon, ranks, possibly failover

### Network issues
- Check public/cluster networks configured
- Ping between nodes
- Check firewalls/iptables
- Verify MTU

## Log Locations
- **cephadm**: `cephadm logs` or container logs
- **Systemd**: `journalctl -u ceph-*`
- **Files**: `/var/log/ceph/*.log` (if file logging enabled)

## Emergency Commands (Lab Only!)
```bash
# Don't use in production without understanding
ceph osd set noout     # prevent automatic out during maintenance
ceph osd unset noout
ceph osd set norebalance
ceph osd unset norebalance
ceph osd set norecover
ceph osd unset norecover
```

## Tips
- Read error messages carefully - they're often descriptive
- Change one thing at a time
- Document fixes
- Google official Ceph tracker/docs first
