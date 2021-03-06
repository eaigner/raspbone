
### Creating the base image on OSX

1. Download Raspbian Lite and unzip the `.img`

        curl -L -O http://downloads.raspberrypi.org/raspbian_lite/images/raspbian_lite-2016-02-09/2016-02-09-raspbian-jessie-lite.zip

    or the latest version if you want. Keep in mind the provisioning script was built for `2016-02-09` and installed system packages might not be the same.

        curl -L -O http://downloads.raspberrypi.org/raspbian_latest

2. Copy the image to the disk

        diskutil list
        diskutil unmountdisk /dev/<sd-root-volume>
        sudo dd if=<path-to-img> of=/dev/<sd-root-volume> bs=2m

### Trimming down the base image

After your PI is reachable on the network, run the `provision.yml` playbook to
remove unwanted packages. The `,` at the end of the IP is necessary!

        ansible-playbook -i "<raspberrypi-ip>," provision.yml -k

This will reduce your used disk space from `912M` to `469M`
