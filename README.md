USB Linux
=========

This script creates a minimal Ubuntu Linux distro onto a USB drive, or it can
create an ISO file. The purpose of this distro is to create an initial
Winsync installation medium. The Winsync server scripts will then automatically
kick in and begin installing Windows and Winsync with minimal user intervention.

This distro is also used to access machines that have a broken OS. To that end
it comes with a LXDE, Ice Weasel, and Filezilla. To save RAM they are not
started by default (see **$EXTRAS** below).

The created distro has several features. The most important of which is it
loads completely into RAM. This means that it takes about 30 seconds from
POST until you can remove the USB drive from the computer. You will be able
to access all the capabilities of the distro without the need for the USB
drive. Generally, this will take only a few hundred megabytes of RAM.

To optimize the RAM loading, the distro is kept very minimal. Only packages
absolutely needed for to complete its mission are installed. You can install
additional packages while the system is running. The available RAM is a
limitation though.

Usage
-----

This is basically just a very long bash script. You will probably need to
adjust the variable values at the top of the script. After that simply run
the script as the root user. Note, this script relies on the underlying OS being
Debian Linux or a derivative (i.e. Debian, Ubuntu, Mint, etc).

If you want to install the script to a USB drive, simply provide the device
file's name. The script does some error checking to make sure that the provided
file is, in fact, a USB block device.

```bash
$ sudo ./install-usb /dev/sdc
```

The script can also create ISO files. I use an ISO of the system so that I
can test under VirtualBox, which will not boot from the USB drive.
Simply pass in a file path ending in .iso, and the script will do the right
thing.

```bash
$ sudo ./install-usb some/path/usb.iso
```

Important Variables
-------------------

Every computer system is different. With this in mind, the script can be easily
configured by simply changing the values of several variables located at the
beginning of the script.

* **$HTTP_CLIENT_SCRIPT** - Installation of client OS's to the hard drive is
handled by a separate script. We do not want to recreate the USB drive OS just
to update the script. So the process is configured to download the script
when tty1 logs in after boot. This variable holds the client installation
script URL.
* **$EXTRAS** - This is a list of extra packages to install beyond the bare
minimum system. These packages should make using the system much more
convenient.
* **$CHROOT** - This variable will hold the location of the directory we are
going to install the minimal system into. We will later chroot into the
environment. The path used does not matter, except be on a partition that has
several hundred megabytes of space. For example, /media/chroot, or
/home/me/chroot will work fine. The script will empty this directory when it
is executed.
* **$ISO_BUILD** - When creating an ISO file, a temporary filesystem must be
created in the host. This is the location where these files will reside. The
path used does not matter, except be on a partition that has several hundred
megabytes of space. The script will empty this directory when it is executed.
* **$ARCH** - This variable's value tells us what type of architecture we are
going to install, e.g. i386, amd64, etc.
* **$CODE_NAME** - This variable tells us what version of system we are
installing. This is done by providing the adjective in the distro's version
code name. Note, this value is case sensitive, always use lower case. For
example, "saucy" or "raring".
* **$MIRROR** - This variable will hold our primary repository. You can
use any valid Ubuntu mirror. By default this value uses the main
"http://archive.ubuntu.com/ubuntu" mirror.
* **$SEC_MIRROR** - This variable is the URL of the security updates mirror. The
value included in the script actually calculates the value based on the
**$MIRROR** variable's value.
* **$KERNEL** - This variable holds the name of the kernel package to install.
* **$HEADERS** - This variable holds the name of the kernel headers package to
install. The actual value is calculated from the value based on the
**$KERNEL** variable's value.

Changelog
---------

**v2.0**
* Removed default files from the script itself. Instead they are now actual
files in the def-files directory. This shortened the script up considerably.
* The script now creates ISO files as well as installing onto a USB. This makes
testing using VirtualBox easier.
* Switch from Debian to Ubuntu as the installed OS.
* Fixed several bugs.
