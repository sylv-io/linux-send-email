# linux-send-email

git-format-patch archive for linux upstreaming

## Guides/Documentation

### General

* [Linux Kernel patch submission checklist](https://www.kernel.org/doc/html/latest/process/submit-checklist.html)
* [Submitting patches: the essential guide to getting your code into the kernel](https://www.kernel.org/doc/html/latest/process/submitting-patches.html)
* [Linux kernel coding style](https://www.kernel.org/doc/html/latest/process/coding-style.html)
* [Creating and Editing patches for the Linux Kernel with git](https://carlosedp.medium.com/creating-and-editing-patches-for-the-linux-kernel-with-git-91feda0c1534)

### hwmon

* [LIST: Linux Hardware Monitoring](https://www.spinics.net/lists/linux-hwmon/)
* [How to Get Your Patch Accepted Into the Hwmon Subsystem](https://www.kernel.org/doc/html/latest/hwmon/submitting-patches.html)


## Configuration

append to ~/.gitconfig
```
[sendemail]
        from = Marcello Sylvester Bauer <sylv@sylv.io>
        smtpuser = sylv@sylv.io
        smtpserver = smtp.mailbox.org
        smtpencryption = tls
        smtpserverport = 587
        chainreplyto = false
        tocover = true
        cccover = true
[sendemail.linux]
    tocmd = "`pwd`/scripts/get_maintainer.pl --nogit --nogit-fallback --norolestats --nol"
    cccmd = "`pwd`/scripts/get_maintainer.pl --nogit --nogit-fallback --norolestats --nom"
```

## Send Patches

Example:
```
# setup
DIR=../linux-send-email
TREE=hwmon
SET=max6639
VERSION=1
BASE=hwmon-next

# 1. format patch
git format-patch -o $DIR/$TREE/$SET/v$VERSION --cover-letter -v $VERSION -n --thread=shallow $BASE..HEAD

# 2. edit cover letter

vim $DIR/$TREE/$SET/v$VERSION/v$VERSION-0000*

# send patches
git send-email --identity=linux $DIR/$TREE/$SET/v$VERSION/
```
