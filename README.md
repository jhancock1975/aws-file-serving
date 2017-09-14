# aws sshfs
Originally I thought I would install an NFS server on my EC2 instance and then mount a file system from my home network - local host is on a private IP.

After installing service on the server side and a client on the client side, mount command did not work to mount the remote file system.

The error in the terminal was a timeout.

`dmesg|tail` shows this error 

`NFS: nfs4_discover_server_trunking unhandled error -512. Exiting with error EIO`

So I did, 
`sudo apt install sshfs`

Then 
`sshfs  ubuntu@23.22.50.118:/home/ubuntu ~/mnt`

I am able to use files under ~/mnt as if they are local files, which is the desired result.

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

! must install nfs-common on client
