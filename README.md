# gcsfuse-config
Google Cloud Storage FUSE plugin install and setup

## Install Python 2.7 on CentOS 6.5
```
sudo yum update;
sudo yum install centos-release-scl;
sudo yum install python27;

```
Add the following to ~/.bashrc to enable Python2.7
```
# Enable Python 2.7
source /opt/rh/python27/enable
```

## Install gcsfuse
1. Configure the gcsfuse repo:
```
sudo tee /etc/yum.repos.d/gcsfuse.repo > /dev/null <<EOF
[gcsfuse]
name=gcsfuse (packages.cloud.google.com)
baseurl=https://packages.cloud.google.com/yum/repos/gcsfuse-el7-x86_64
enabled=1
gpgcheck=1
repo_gpgcheck=1
gpgkey=https://packages.cloud.google.com/yum/doc/yum-key.gpg
       https://packages.cloud.google.com/yum/doc/rpm-package-key.gpg
EOF
```
2.  Make the system aware of the new repo:
```
sudo yum update
sudo yum install -y gcsfuse
```

## Setup gcsfuse with mount
1.  Add certification (JSON format) to system
2.  Add the following to `/etc/fstab`:
```
bucket-name /mount/folder gcsfuse rw,noauto,user,key_file=/path/to/cert.json
```
3.  Change permission of `/bin/fusermount`
```
sudo chmod 6755 /bin/fusermount
```
