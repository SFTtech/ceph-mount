CephFS Standalone Mount Tool
============================

CephFS is part of the Linux kernel, so you don't need the userland Ceph packages installed.

Usually, `/sbin/mount.ceph` is shipped by the Ceph packages written in C++.
This standalone pure Python implementation mimics the `mount.ceph` functionality.

With this script you can mount Ceph e.g. with systemd mount units without installing Ceph.

This tool can upload the secret key into the kernel keyring and mount your CephFS.

`mount.ceph` is the "high-level" mount helper,
`cephfs_mount` is the "low-level" tool which actually mounts.


### Installation

`mount -t ceph` really only calls `/sbin/mount.ceph`, so we need to provide that file.

Way 1:
* Clone the repo e.g. to `/opt/ceph-mount` via `git clone https://github.com/SFTtech/ceph-mount /opt/ceph-mount`
* Symlink `/sbin/mount.ceph -> /opt/ceph-mount/mount.ceph`

Way 2:
* Install `mount.ceph` and `cephfs_mount` to `/usr/bin/`
* Symlink `/sbin/mount.ceph -> /usr/bin/mount.ceph`

Way 3:
* Install `mount.ceph` and `cephfs_mount` to `/sbin/`


### Examples

`/sbin/mount.ceph` is called by `mount` when the fstype is `ceph`,
so that's how an entry in `/etc/fstab` still makes use of this tool.

Likely `mount.ceph --help` or `cephfs_mount --help` will guide you.

Example `/etc/fstab` entry:

```
mon1.ceph.lol,mon2.ceph.lol,mon3.ceph.lol:/your/path /your/mountpoint ceph rw,noatime,name=your-auth-name,secretfile=/etc/ceph/ceph.client.your-auth-name.keyring,_netdev 0 0
```

Example `mount` invocation:

```
mount -t ceph -o rw,noatime,name=your-auth-name,secretfile=/etc/ceph/ceph.client.your-auth-name.keyring mon1.ceph.lol,mon2.ceph.lol,mon3.ceph.lol:/your/path /your/mountpoint
```

Example `./cephfs_mount` invocation:

```
./cephfs_mount --user your-auth-name mon1.ceph.lol,mon2.ceph.lo,mon3.ceph.lol:/path /destination
# this looks in /etc/ceph/ceph.client.your-auth-name.keyring for the key
# if you write :/path only, it uses the MONs from /etc/ceph/ceph.conf
```

If in doubt, look at the source code :)


### Contact

If you have questions, suggestions, encounter any problem,
please join our Matrix or IRC channel and ask!

```
#sfttech:matrix.org
irc.freenode.net #sfttech
```


### License

License: GPL version 3 (or any later version)
