To create an NFS server
=======================

    gcloud deployment-manager deployments create <deployment name> --config config.jinja --properties zone=<str>,machineType=<str>,dataDiskSizeGb=<int>,storagePoolName=<str>,network=<str>,adminPassword=<str>,dataDiskType=<str>

E.g.

    gcloud deployment-manager deployments create test-nfs-deployment --config config.jinja --properties zone=us-east1-c,machineType=n1-highmem-2,dataDiskSizeGb=2000,storagePoolName=test-storage-dir,network=default,adminPassword=highsecuritypassword,dataDiskType=pd-standard

Will create an NFS server with hostname test-nfs-deployment-vm

Add the --preview flag to first preview the resources before proceeding.  

See the docs : https://cloud.google.com/sdk/gcloud/reference/deployment-manager/deployments/create  

To see the status of a deployment
=================================

    gcloud deployment-manager deployments describe <deployment name>

To delete an NFS server
=======================

    gcloud deployment-manager deployments delete <deployment name>

The Coordinator
===============

The NFS server deployment from google creates a coordiantion server to track the deployment.

This server automatically deletes itself when it realizes all other instances are in a terminal state.

From monitor_deployment.sh:

    # dc_monitor_deployment
    #
    # Deployment Coordinator driver script that gets the name of the deployment
    # from instance metadata and then calls monitor_deployment.sh on it.
    #
    # Once completed, this Deployment Coordinator deletes itself.

If you are interested in what the coordinator is doing, ssh on the box and take a look at its start up scripts.
