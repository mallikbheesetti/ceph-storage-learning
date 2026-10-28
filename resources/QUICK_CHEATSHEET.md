# Ceph Quick Cheatsheet

## Cluster Status
```bash
ceph -s                    # Status summary
ceph health detail         # Detailed health
ceph -w                    # Watch live
ceph df                    # Disk usage
ceph versions              # Component versions
```

## MON
```bash
ceph mon stat
ceph mon dump
ceph quorum_status
```

## OSD
```bash
ceph osd tree
ceph osd stat
ceph osd df
ceph osd out osd.N
ceph osd in osd.N
```

## Pools & PGs
```bash
ceph osd pool ls detail
ceph osd pool create <pool> <pg_num> <pgp_num>
ceph osd pool delete <pool> <pool> --yes-i-really-really-mean-it
ceph pg stat
ceph pg dump_stuck
```

## Auth
```bash
ceph auth list
ceph auth get-or-create <entity> <caps>
ceph auth del <entity>
```

## RBD
```bash
rbd create <pool>/<img> --size <size>
rbd list <pool>
rbd map <pool>/<img>
rbd unmap /dev/rbdX
rbd snap create <pool>/<img>@<snap>
rbd snap list <pool>/<img>
```

## CephFS
```bash
ceph fs ls
ceph fs status
ceph mds stat
mount -t ceph mon1:6789:/ /mnt -o name=admin,secretfile=...
```

## RGW
```bash
radosgw-admin user create --uid=... --display-name=...
radosgw-admin bucket list --uid=...
```

## Config
```bash
ceph config dump
ceph config get <daemon> <key>
ceph config set <who> <key> <value>
```

## Debugging
```bash
journalctl -u ceph-<daemon>@<id> -n 100
ceph pg <pgid> query
ceph osd find <id>
```
