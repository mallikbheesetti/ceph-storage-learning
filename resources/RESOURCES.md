# Curated Resources

## Official Documentation
- [Ceph.io Official Site](https://ceph.io/) - Main site, news, community
- [Ceph Documentation](https://docs.ceph.com/) - Official docs (latest)
- [Ceph Installation Guide](https://docs.ceph.com/en/latest/install/)
- [Ceph Administration Guide](https://docs.ceph.com/en/latest/rados/operations/)
- [RBD Documentation](https://docs.ceph.com/en/latest/rbd/)
- [CephFS Documentation](https://docs.ceph.com/en/latest/cephfs/)
- [RGW Documentation](https://docs.ceph.com/en/latest/radosgw/)

## Red Hat Ceph Storage Docs (Great for structured learning)
- [Red Hat Ceph Storage Documentation](https://access.redhat.com/documentation/en-us/red_hat_ceph_storage)
- Many concepts are universal even if using upstream Ceph

## Learning Platforms & Videos
- [Ceph YouTube Channel](https://www.youtube.com/@CephStorage)
- [Ceph Days Presentations](https://ceph.io/en/community/ceph-days/)
- [Class Central - Ceph Courses](https://www.classcentral.com/subject/ceph)
- [OpenInfra Foundation](https://openinfra.org/)

## Books & Papers
- [Ceph Cookbook (various editions)](https://www.oreilly.com/)
- [Mastering Ceph](https://www.packtpub.com/)
- CRUSH paper: [CRUSH: Controlled, Scalable, Decentralized Placement of Replicated Data](https://ceph.io/assets/pdfs/weil-crush-sc06.pdf)

## Tools
- [cephadm](https://docs.ceph.com/en/latest/cephadm/)
- [Rook](https://rook.io/)
- [ceph-csi](https://github.com/ceph/ceph-csi)
- [Prometheus Ceph Exporter](https://github.com/digitalocean/ceph_exporter) / MGR prometheus module

## Communities
- [Ceph Mailing Lists](https://ceph.io/en/community/connect/)
- [Ceph Slack/Matrix](https://ceph.io/en/community/connect/)
- [Reddit r/ceph](https://www.reddit.com/r/ceph/)
- [Ceph GitHub](https://github.com/ceph/ceph)

## Cheat Sheets
- [Ceph Cheat Sheet (DigitalOcean)](https://docs.digitalocean.com/products/volumes/resources/ceph-cheat-sheet/)
- Keep your own in this repo as you learn!

## Practice Clusters (if no hardware)
- Use VMs locally (cheapest)
- Some cloud providers have Ceph, but can be costly
- [Vagrant Ceph examples](https://github.com/ceph/ceph-ansible/tree/main/vagrant_variables.yml.example) (if using ceph-ansible)

## Tips
- Focus on official Ceph docs for your target version
- Understand concepts (PGs, CRUSH) deeply - they apply everywhere
- Hands-on > theory for retention
- Break things and fix them
