USB Linux
=========

This script creates a minimal Debian Linux distro onto a USB drive.
The purpose of this distro is to create an initial Winsync installation medium.
The Winsync server scripts will then automatically kick in and begin installing
Windows and Winsync with minimal user intervention.

This distro is also used to access machines that have a broken OS. To that end
it comes with a LXDE and Ice Weasel. To save RAM they are not started by
default.

The created distro has several features. The most important of which is it
loads completely into RAM. This means that it takes about 30 seconds from
power on until you can remove the USB drive from the computer. You will be able
to access all the capabilities of the distro without the need for the USB
drive. Generally, this will take only a few hundred megabytes of RAM.

To actualize the RAM loading, the distro is kept very minimal. Only packages
absolutely needed for to complete its mission are installed.

Usage
-----

This is basically just a very long bash script. You will probably need to
adjust the variable values at the top of the script. After that simply run
the script as the root user. Note, this script relies on the underlying OS being
Debian Linux or a derivative (i.e. Ubuntu, Mint, etc).

```bash
$ sudo ./install-usb
```

Important Variables
-------------------

Every computer system is different. Toward this end, the script can be easily
configured by simply changing the values of several variables located at the
beginning of the script.

* **$DEV** - This variable corresponds to the USB device file for the drive you
wish to install the distro on. For example, /dev/sdb
* **$CHROOT** - This variable will hold the location of the directory we are going
to install the minimal system into. We will later chroot into the environment.
The path used does not matter, except it should point to an non-existent
directory (we will create it later) on a partition that has several hundred
megabytes of space. For example, /media/chroot, or /home/me/chroot
* **$ARCH** - We need a variable that tells us what type of architecture we are
going to install, e.g. i386, amd64, etc.
* **$CODE_NAME** - This variable tells us what version of system we are
installing. This is done by providing the adjective in the distro's version
code name. Note, this value is case sensitive, always use lower case. For
example, "testing" or "stable".
* **$MNT** - This variable will hold the directory we will use to mount our USB
device onto. We have to mount the USB so that we can copy the filesystem
onto it. For example, /mnt or /media/usb.
* **$MIRROR** - This variable that will hold our primary repository. You can use any
valid debian mirror. By default this value uses the main
"http://http.us.debian.org/debian/" mirror.
* **$HTTP_CLIENT_SCRIPT** - Installation to the hard drive is handled by a separate
script. We do not want to recreate the USB drive OS just to update the script.
So the process is configured to download the script when tty1 logs in after
boot. This variable holds the client installation script URL.
* **$KERNEL** - This variable holds the name of the kernel to install.

