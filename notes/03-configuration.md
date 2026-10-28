# 03 - Configuration

## Configuration Sources (Precedence)
From lowest to highest priority:
1. Built-in defaults
2. Monitor's central configuration database (`ceph config dump`)
3. Local `ceph.conf` file
4. Command-line/runtime overrides

## Config File Location
- `/etc/ceph/ceph.conf` (common)
- Can be specified with `-c` or `--conf`

## Basic Structure
```ini
[global]
fsid = ...
mon_host = ...
auth_cluster_required = cephx
auth_service_required = cephx
auth_client_required = cephx

[mon]
mon_data = /var/lib/ceph/mon/ceph-$id

[osd]
osd_data = /var/lib/ceph/osd/ceph-$id
osd_journal_size = 5120

[mds]
...

[client.rgw.*]
...
```

## Key Settings

### Network
```ini
[global]
public_network = 192.168.1.0/24
cluster_network = 10.0.0.0/24  # for replication/recovery
```

### Authentication
```ini
auth_cluster_required = cephx
auth_service_required = cephx
auth_client_required = cephx
```

### Monitors
```ini
[mon]
mon_warn_on_low_pools = true
```

### OSDs / BlueStore
```ini
[osd]
osd_memory_target = 4G  # tune by RAM
```

## Managing Config with CLI
```bash
ceph config dump                    # show all effective config
ceph config get osd.1 osd_memory_target
ceph config set global mon_allow_pool_delete true
ceph config show osd.1             # show config for daemon
ceph config assimilate-conf -i ceph.conf  # push conf to mon
```

## Keyrings
- Located in `/etc/ceph/` (e.g., `ceph.client.admin.keyring`)
- Contain auth keys and capabilities
- Protect with proper permissions (0600)

## Common Tuning Considerations
- Separate public/cluster networks for performance/isolation
- Tune PG count for pools
- Adjust recovery/throttling if needed
- Use BlueStore
- Consider journaling/WAL/db sizes

## Exercises
- [ ] View effective configuration
- [ ] Change a setting via CLI and verify
- [ ] Understand public vs cluster network
- [ ] Create/edit ceph.conf and apply
- [ ] Review keyring permissions
