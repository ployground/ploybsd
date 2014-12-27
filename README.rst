PloyBSD
=======

*PloyBSD* is a `NanoBSD <https://www.freebsd.org/doc/en/articles/nanobsd/index.html>`_ based `FreeBSD <https://www.freebsd.org>`_ distribution pre-configured to act as a host for `bsdploy <http://docs.bsdploy.net/en/latest/>`_.


Building PloyBSD
----------------

PloyBSD uses combines two existing approaches, namely mfsBSD and nanobsd by using the latter to assemble a bootable image using binary installation packages provided by the former. The end result of which is a disk image that can be

 - used to boot a virtual machine
 - can be written onto a USB stick or disk partition to boot an actual machine


Bootstrapping the build environment
+++++++++++++++++++++++++++++++++++

Building PloyBSD represents a "chicken and egg" situation. To this end we have created an Ansible role that configures a FreeBSD host as a suitable build platform along with a ploy configuration that creates a vanilla FreeBSD 10.1 VirtualBox instance.

To use it, first download the mfsBSD installation medium at http://mfsbsd.vx.sk (use the so-called *special edition* because it contains the installation packages). Make sure you end up with an image named ``~/Downloads/mfsbsd-se-10.1-RELEASE-amd64.iso``.

Then::

    ploy start nanobuild-vbox
    ploy bootstrap
    ploy configure nanobuild


Fetching sources
++++++++++++++++

The easiest way to obtain nanobsd itself is to download the FreeBSD sources, because it's part of the official tools and while it's a bit overkill to download the entire sources, it's the easiest way to ensure that your nanobsd edition matches your system.

In this playbook we download the corrsponding 10.1 release sources like so::

    ploy ssh nanobuild

    root@nanobuild:~ svnup release10


Building
++++++++

Now you can commence with building::

    root@nanobuild:~ cd /FreeBSD
    root@nanobuild:/FreeBSD # sh release10/src/tools/tools/nanobsd/nanobsd.sh -vc ploybsd.conf
