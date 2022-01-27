# ansible-jenkins
This is an [ansible](http://ansible.com/) playbook to install and
configure [Jenkins-CI](http://jenkins-ci.org/).

The playbook will install NGINX, Docker, a local-only
SMTP server and Jenkins. It will also install Docker-maintenance cron
jobs and Jenkins-backup scripts to S3.

This playbook assumes that the instance is behind an elb and the elb will
do its SSL termination. The ssl certificate can be obtained using AWS ACM
or can be manually uploaded

This playbook is a rework of the [ee-infra-jenkins](https://github.com/mozmeao/ee-infra-jenkins)

## Build your own
1. SSH to host you want to run this
2. Install `git` and `ansible`
3. Clone this repository to a location
4. Run the playbook
```
ansible-playbook site.yml -e "nginx_htpasswd=YourPasswordHere jenkins_backup_bucket=BucketNameHere jenkins_backup_dms=deadmanssitchurl jenkins_backup_directory=backupdirpath papertrail_host=papertrailurl papertrail_port=papertrailport"
```

Currently this playbook is being used as part of an autoscaling group userdata that clones and runs this playbook on boot.

## Jenkins backups

This playbook expects that you use the [ThinBackup](https://wiki.jenkins-ci.org/display/JENKINS/thinBackup) Jenkins plugin and that you save backups in `/data/backups`.
