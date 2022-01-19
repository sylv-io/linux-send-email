# linux-send-email
git-format-patch archive for linux upstreaming

## Guides/Documentation

### General

* [Linux Kernel patch submission checklist](https://www.kernel.org/doc/html/latest/process/submit-checklist.html)
* [Submitting Drivers For The Linux Kernel](https://www.kernel.org/doc/html/latest/process/submitting-drivers.html)
* [Submitting patches: the essential guide to getting your code into the kernel](https://www.kernel.org/doc/html/latest/process/submitting-patches.html)
* [Linux kernel coding style](https://www.kernel.org/doc/html/latest/process/coding-style.html)

* [Creating and Editing patches for the Linux Kernel with git](https://carlosedp.medium.com/creating-and-editing-patches-for-the-linux-kernel-with-git-91feda0c1534)

### hwmon

* [LIST: Linux Hardware Monitoring](https://www.spinics.net/lists/linux-hwmon/)
* [How to Get Your Patch Accepted Into the Hwmon Subsystem](https://www.kernel.org/doc/html/latest/hwmon/submitting-patches.html)

## Commands

```
# setup
DIR=send-email
SET=max6639
VERSION=1
HEAD=upstream_$SET
BASE=hwmon-next
MAILING_LIST=linux-hwmon@vger.kernel.org

# 1. format patch
git format-patch -o $DIR/$SET --cover-letter -v $VERSION -n --thread=shallow $BASE..$HEAD

# 2. edit cover letter

vim $DIR/$SET/v$VERSION-0000*

# edit each patch and add maintainer

#for each patch file:
scripts/get_maintainer.pl --no-rolestats $DIR/$SET/$PATCH_FILE
#append maintainer
vim $DIR/$SET/$PATCH_FILE

# send patches
git send-email $DIR/$SET/$VERSION-* --to $MAILING_LIST
```
