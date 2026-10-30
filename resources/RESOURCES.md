# Curated Resources

## Red Hat Ceph Certification
- [EX260 Exam Page](https://www.redhat.com/en/services/training/ex260-red-hat-certified-specialist-in-ceph-cloud-storage-exam) - Official exam description, objectives, format
- [Red Hat Certified Specialist in Ceph Cloud Storage](https://www.redhat.com/en/services/certification/rhcs-ceph-cloud-storage) - Credential overview and skills
- [CL260 - Cloud Storage with Red Hat Ceph Storage](https://catalog.redhat.com/search?searchType=learning&q=CL260) - Recommended training course (catalog search)
- [Red Hat Training Policies](https://www.redhat.com/en/about/red-hat-training-policies) - Exam delivery, retakes, and rules
- [Certification Renewal](https://www.redhat.com/en/services/certification/renewal) - 3-year validity and renewal paths
- [RHCA - Enterprise Linux](https://www.redhat.com/en/services/certification/red-hat-certified-architect-in-enterprise-linux) - Architect requirements; EX260 counts as a specialist exam
- [Certification Exam Objectives by Version (PDF)](https://training-lms.redhat.com/public_content/redhat/training/Red%20Hat%20Certification%20Exam%20Objectives%20by%20Version.pdf) - Official objective list per version
- [Credly Badge](https://www.credly.com/org/red-hat-inc/badge/red-hat-certified-specialist-in-ceph-cloud-storage) - Digital credential information
- This repo: [Certification Path](../certification/CERTIFICATION_PATH.md) and [Mock Exams](../certification/MOCK_EXAMS.md)

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
