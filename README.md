Dependencies
============

* [python gcp sdk](https://cloud.google.com/compute/docs/tutorials/python-guide#cloud-sdk)
```
pip install --upgrade google-api-python-client 
``` 
 
To create an NFS server
=======================

    ./gcloudnfs create --project <project> --zone <zone> --network <network> --machine-type <machine-type> --server-name <server-name> --data-disk-name <data-disk-name> --data-disk-type <data-disk-type> --data-disk-size <data-disk-size>

    E.g.

    ./gcloudnfs create --project my_project --zone us-east1-c --network default --machine-type n1-standard-1 --server-name test-server --data-disk-name test-data-disk --data-disk-type pd-standard --data-disk-size 2000

To destroy an NFS server
========================

    ./gcloudnfs destroy --project <project> --zone <zone> --network <network> --data-disk-name <data-disk-name> --server-name <server-name>

    E.g.

    ./gcloudnfs destroy --project my_project --zone us-east1-c --network default --data-disk-name test-data-disk --server-name test-server

Reusing an existing disk
========================

Passing the `--reuse-data-disk` flag to the create and destroy commands is necessary to reuse a disk. 

Passing `--reuse-data-disk` to create causes the command to skip disk creation, instead attaching the existing disk named `--data-disk-name` to the existing instance.

Passing `--reuse-data-disk` to destroy causes the command to skip disk destruction, saving the disk for later use.

Future Performance Improvements
===============================

* Add a dedicated ZIL device.
* Optimize ARC cache size
* Add dedicated SSDs for L2ARC cache
* Add more disks and use striping with parity across the disks. 
* optimize async write percentages 
* If NFS is the bottleneck, try optimizations here : http://nfs.sourceforge.net/nfs-howto/ar01s05.html
