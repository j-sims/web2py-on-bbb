### web2py-on-bbb
Guide for installing Web2Py on a BeagleBoneBlack

#### Resources
Image: Ubuntu <br>
Documentation: http://elinux.org/BeagleBoardUbuntu

Ubuntu 14.04 Flasher Image: https://rcn-ee.com/rootfs/2015-10-09/flasher/BBB-eMMC-flasher-ubuntu-14.04.3-console-armhf-2015-10-09-2gb.img.xz

# Steps
- Flash with Ubuntu
- Power up connected to ethernet
- apt-get update {failed}
-- resolv.conf pointed to nameserver 127.0.0.1
-- Should have picked up via dhcp
-- manually edited
-- will investigate later
-- re-ran {success}
- apt-get upgrade {success - couple odd errors}
    update-initramfs: Generating /boot/initrd.img-4.2.3-armv7-x2
    WARNING: missing /lib/modules/4.2.3-armv7-x2
    Device driver support needs thus be built-in linux image!
    depmod: ERROR: could not open directory /lib/modules/4.2.3-armv7-x2: No such file or directory
    depmod: FATAL: could not search modules: No such file or directory
    depmod: WARNING: could not open /tmp/mkinitramfs_CWlPk5/lib/modules/4.2.3-armv7-x2/modules.order: No such file or directory
    depmod: WARNING: could not open /tmp/mkinitramfs_CWlPk5/lib/modules/4.2.3-armv7-x2/modules.builtin: No such file or directory
- apt-get -y install curl
- cd /usr/lib
- apt-get install unzip
- wget http://www.web2py.com/examples/static/web2py_src.zip
- unzip web2py_src.zip
- ln -s /usr/lib/web2py/scripts/web2py.ubuntu.sh /etc/init.d/web2py
- sudo update-rc.d web2py defaults
- edit script and add port, interface and change user
-- vi /etc/init.d/web2py
    DAEMON_ARGS="web2py.py --password=<recycle> --pid_filename=$PIDFILE -p 8080 -i 0.0.0.0"
    DAEMON_USER=root
- Manually start to specify password
-- /etc/init.d/web2py start
- rm /etc/issue /etc/issue.net
- set the admin password
-- replace "<recycle>" in /etc/init.d/web2py
-- /etc/init.d/web2py start
-- /etc/init.d/web2py stop
-- replace yourpass with "<recycle>"
-- /etc/init.d/web2py start





