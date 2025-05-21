# NFS Server Setup and Client Mount

This guide outlines how to set up an NFS server on Ubuntu, configure a shared directory, and mount it on a client machine.

## Step 1: Set Up NFS Server

Install and configure an NFS server to share a directory for use, such as for PostgreSQL data.

### Install NFS Server
Update the package list and install the NFS kernel server.

```bash
sudo apt update
sudo apt install nfs-kernel-server
```

### Create Shared Directory
Set up a directory for sharing, with appropriate permissions for NFS.

```bash
sudo mkdir -p /srv/nfs/postgres
sudo chown nobody:nogroup /srv/nfs/postgres
sudo chmod 777 /srv/nfs/postgres
```

### Configure /etc/exports
Add the directory to the NFS exports file, specifying client IPs and permissions (e.g., read/write, sync).

```bash
echo "/srv/nfs/postgres 172.16.69.56(rw,sync,no_subtree_check,no_root_squash) 172.16.69.57(rw,sync,no_subtree_check,no_root_squash)" | sudo tee -a /etc/exports
```

### Activate NFS Service
Apply the export configuration and restart the NFS service.

```bash
sudo exportfs -rav
sudo systemctl restart nfs-kernel-server
```

## Step 2: Connect Client to NFS Server

Configure a client machine to mount the NFS share.

### Install NFS Client
Install the NFS client package on the client machine.

```bash
sudo apt update
sudo apt install nfs-common
```

### Mount the NFS Share
Mount the shared directory from the NFS server to a local directory (e.g., /mnt).

```bash
sudo mount -t nfs <nfs-server-ip>:/srv/nfs/postgres /mnt
```

Replace `<nfs-server-ip>` with the actual IP address of the NFS server.

## Troubleshooting
If the mount fails, verify the NFS export configuration on the server.

```bash
sudo exportfs -v
```

This command lists active exports and helps confirm if the directory is correctly shared.
