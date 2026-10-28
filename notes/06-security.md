# 06 - Security

## Authentication & Authorization (CephX)
CephX provides mutual authentication between clients/daemons.

- Keys stored in keyrings
- Each entity has ID and secret key
- Capabilities define permissions

### Manage auth
```bash
ceph auth list
ceph auth get client.admin
ceph auth add client.foo mon 'allow r' osd 'allow rw pool=data'
ceph auth caps client.foo mon 'allow r' osd 'allow rwx pool=data'
ceph auth del client.foo
```

### Common capability patterns
```text
mon 'allow *'                    # full monitor access
mon 'allow r'                    # read-only
osd 'allow rwx pool=mypool'     # full access to pool
osd 'allow class-read object_prefix rbd_children'  # specific
```

## Network Security
- **Separate networks**: Use public_network and cluster_network
- **Firewall**: Restrict ports (MON 3300/6789, OSD, MGR, RGW)
- **Bind to specific IPs**
- **Avoid exposing to internet directly**

**Default ports (varies by version)**:
- MON: 6789 (legacy), 3300 (msgr2)
- OSD/MGR/MDS: ephemeral or configured
- RGW: 7480 (default), or 80/443 behind proxy

## Encryption
- **In-transit**: Messenger v2 supports encryption (`ms_bind_msgr2`, secure mode)
- **At-rest**: OSD level encryption depends on deployment (dm-crypt, or BlueStore encryption features)
- **TLS for RGW**: Terminate TLS at RGW or reverse proxy (HAProxy/Nginx)

## RGW Security
- **User management**: Per user keys
- **Bucket policies / ACLs**: Control access
- **S3 signatures**: Authenticated requests
- **CORS**: Configure if needed
- **TLS**: Use HTTPS
- **LDAP/Keystone integration**: For auth backends (advanced)

```bash
radosgw-admin user info --uid=testuser
radosgw-admin caps add --uid=testuser --caps="buckets=*"
```

## Key Management Best Practices
- Rotate keys periodically
- Use least privilege (minimal caps)
- Store keyrings securely (0600, owned by ceph user)
- Don't share admin keys
- Use separate clients per application

## Hardening Checklist
- [ ] Enable CephX everywhere
- [ ] Separate public/cluster networks
- [ ] Configure firewall rules
- [ ] Use Messenger v2 where possible
- [ ] Enable TLS for RGW
- [ ] Limit admin key usage
- [ ] Apply least privilege to clients
- [ ] Keep Ceph updated
- [ ] Monitor auth failures
- [ ] Secure etc/ceph and keyrings

## Exercises
- [ ] Create a read-only client
- [ ] Create a pool-restricted client
- [ ] Review network binding
- [ ] Configure RGW with TLS (lab)
- [ ] Audit auth list and clean up unused keys
