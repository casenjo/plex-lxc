
# Plex LXC Container

### Proxmox Host Setup (if using SMB)
Run `apt install -y cifs-utils` in order to allow the LXC container to use SMB

### On the Plex LXC container

#### 1. Create /plex folders owned by your non-root user

`sudo mkdir -p /plex/{database,transcode,media} && sudo chown -R $USER:$USER /plex`

#### 2. Create Plex's mount directories

  `mkdir /plex/media/{mount_name_0,mount_name_1,mount_name_n}`

#### 3. Add mount directories to `/etc/fstab`
```
# Sample /etc/fstab

## RAM transcode (4 GB)
tmpfs  /plex/transcode  tmpfs  rw,size=4G  0   0

## Sample CIFS mount where the folder has spaces (note the \040 to represent the space) and use of credential files
//X.X.X.X/Media/TV\040Shows  /plex/media/mount_name_0 cifs credentials=/etc/credentials-file,iocharset=utf8,uid=1000,gid=1000,dir_mode=0755,file_mode=0755
```

### Configure the env file by copying `env.dist` to `.env` and fill in the blanks
