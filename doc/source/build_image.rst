Building an Image
============

Only one image needs to be build for os-disk-config.  The images contains a second disk that is going to be customized by os-disk-config.

The following steps can be used to build images. They should be run as the same
non-root user that was used to install the undercloud from setup.

#. Build the os-disk-config image::

    sudo rm /tmp/svc-map-services
    instack-build-images os-disk-config

#. Load the images into Glance and disable local boot::

    source stackrc
    tripleo load-image -d os-disk-config.qcow2
    nova flavor-key baremetal_compute unset "baremetal:localboot"
