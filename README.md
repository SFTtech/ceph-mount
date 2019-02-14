CephFS Standalone Mount Tool
============================

Standalone pure Python implementation of the `mount.ceph` functionality.
With this script you can mount Ceph with systemd mount units without installing Ceph.

It can upload the secret key into the kernel keyring and mount your CephFS.
This is usually done by the C++ `mount.ceph`, which is part of the Ceph packages.


License: GPL version 3 (or any later version)
