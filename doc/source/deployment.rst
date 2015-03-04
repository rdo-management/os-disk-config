Deployment
=======================

Deploy your overcloud with the customized disk::

    heat stack-create overcloud -e $HOME/instack-undercloud/heat-templates/resource-registry.yaml -f $HOME/instack-undercloud/heat-templates/os-disk-config-deployment.yaml -P "node_count=2" -P 'disk_config={"partitions": [{"name": "test1","disks":["vda"],"filesystem": "ext4","size": "1 GiB","type": "standard","mountpoint": "/mnt/test"}], "version": "0.0.1"}'

To reset the extra disks attached to the instances, make sure all the vms are shut down, then run as root::
    rm -f /var/lib/libvirt/images/baremetal_extra_*.qcow2
    for i in `seq 0 3`; do qemu-img create /var/lib/libvirt/images/baremetal_extra_$i.qcow2 10G; done
