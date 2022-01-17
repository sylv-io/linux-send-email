# linux-send-email
git-format-patch archive for linux upstreaming

## Guides

* [Creating and Editing patches for the Linux Kernel with git](https://carlosedp.medium.com/creating-and-editing-patches-for-the-linux-kernel-with-git-91feda0c1534)

## Commands

wip

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
git send-email $DIR/$SET/$VERSION-* --to $MAILING_LIST --to linux-kernel@vger.kernel.org output/$SET/$VERSION-*
```
