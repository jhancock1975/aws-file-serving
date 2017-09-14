# aws-nfs4
notes and configs for running nfs-4 on aws instance

using howto found from google search: https://help.ubuntu.com/community/NFSv4Howto

choosing nfs4 without kerberos
TODO: install with kerberos

commands:
sudo mkdir /export
sudo mkdir /export/users

sudo mount --bind /home/ /export/users 

#add line to /etc/fstab:
/home/users    /export/users   none    bind  0  0 

#add line to /etc/exports
/export        66.249.65.220(rw,fsid=0,no_subtree_check,sync)
/export/users  66.249.65.220(rw,nohide,insecure,no_subtree_che

sudo service nfs-kernel-server restart

#next command didn't work:

sudo service idmapd restart I got an error message like:
Failed to restart idmapd.service: Unit idmapd.service is masked
so I just rebooted the server, that'll show 'em
