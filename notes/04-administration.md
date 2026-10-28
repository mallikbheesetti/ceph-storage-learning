# 04 - Administration

## Cluster Health
```bash
ceph -s                          # summary
ceph status
ceph health
ceph health detail
ceph -w                          # watch live
```

**Health states**: HEALTH_OK, HEALTH_WARN, HEALTH_ERR

## Monitor Management
```bash
ceph mon stat
ceph mon dump
ceph quorum_status --format json-pretty
```

- Maintain odd number for quorum
- Add/remove MONs carefully per docs

## OSD Management
```bash
ceph osd tree
ceph osd stat
ceph osd df
ceph osd perf
ceph osd find <osd-id>
```

### Mark out/in, down/up
```bash
ceph osd out osd.5      # rebalance away
ceph osd in osd.5       # bring back
ceph osd down osd.5
ceph osd up osd.5
```

### Add/remove OSD (general workflow)
1. Prepare disk
2. `ceph-volume lvm create --data /dev/sdb` (or zap/create)
3. Cluster rebalances automatically
4. To remove: out, stop, purge, remove from crush

## Pools & PGs
```bash
ceph osd pool ls detail
ceph pg dump_stuck
ceph pg stat
ceph pg <pgid> query
```

### Create pool
```bash
ceph osd pool create mypool 64 64
ceph osd pool application enable mypool rbd
```

### Set pg_num (careful)
Increasing pg_num causes splitting/rebalancing; follow best practices. Changing requires planning.

## CRUSH Management
```bash
ceph osd crush dump
ceph osd crush tree
ceph osd crush rule ls
```

- Customize CRUSH for failure domains (rack-aware etc.)
- Usually managed via ceph CLI or crushmap

## Authentication (CephX)
```bash
ceph auth list
ceph auth get-or-create client.myuser mon 'allow r' osd 'allow rw pool=mypool'
ceph auth get client.admin
```

Capabilities control access per daemon type/pool.

## MGR & Dashboard
```bash
ceph mgr stat
ceph mgr module ls
ceph mgr module enable dashboard
ceph dashboard set-login-credentials admin <password>
```

## Administration Best Practices
- Monitor health regularly
- Keep MONs odd count
- Watch PG counts
- Plan maintenance windows
- Test changes in lab first
- Back up configs/keyrings/CRUSH maps

## Exercises
- [ ] Check cluster health and interpret status
- [ ] List pools, PGs, understand states
- [ ] Create a user with limited capabilities
- [ ] Explore CRUSH map
- [ ] Manage OSD states (out/in) in lab
