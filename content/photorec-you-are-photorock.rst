Photorec , you are Photorock!
#############################
:date: 2010-09-30 22:31
:category: Gnu/Linux, My Thoughts
:tags: fat32, ntfsundelete, pendrive, photorec, recovery tool, testdisk, ubuntu

Yesterday my ubuntu installation went wrong when i misplaced an
essential lib. Even the tab completion feature in gnome-terminal and cp,
mv commands were not working. Some how i backed up some \*important
files\* i stored in my root filesystem to my usb drive and installed
ubuntu again, and moved back the \*important files\* to root filesystem.
But again ubuntu stopped working after i installed some debs. But this
time before reinstalling ubuntu i forgot to backup the important files
from my root filesystem to the pendrive. I realized this only after the
installation process reached 50% . What to do???. Today classes were
suspended at 12 because of Ayodhya verdict, so came home earlier, sat in
front of the lappy and started googling. While searching i found a tool
named ntfsundelete, but really disppointed when i came to know that it
works only for ntfs filesystems. My pendrive is having Fat32 filesystem.
Again continued searching and found a `blog`_ discussing about a
component of testdisk application named photorec. I ran apt-get install
testdisk and photorec got installed. i ran photorec at the command line
and it told me to run it as root. so ran it as root and it asked me to
select the disk. i selected my pendrive, it needed some info about
parition table and the directory where the recovered files should be
stored which was defaulted to home directory. And it started recovering.
When the recovery process completed there was about 45 directories in my
home directory. After spending some time in searching those directories
i found 4 out of 5 \*important files\*. Four is a lot better than none,
isnt it?.. thanks photorec!

.. _blog: http://cuasan.wordpress.com/2008/03/31/undelete-files-on-a-vfat-partition-in-ubuntu/
