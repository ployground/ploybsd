PloyBSD
=======

*PloyBSD* is a `NanoBSD <https://www.freebsd.org/doc/en/articles/nanobsd/index.html>`_ based `FreeBSD <https://www.freebsd.org>`_ distribution pre-configured to act as a host for `bsdploy <http://docs.bsdploy.net/en/latest/>`_.


Building PloyBSD
----------------

The end result of building PloyBSD is a disk image that can be used to boot a virtual machine or that can be written onto a USB stick to boot an actual machine.

Building PloyBSD represents a sort of "chicken and egg" situation (unless you are the sort of person who has a FreeBSD system with a fresh checkout of its sources lying around).

To this end we have created an Ansible role that configures a FreeBSD host as a suitable build platform along with a ploy configuration that creates a vanilla FreeBSD 10.1 VirtualBox instance.

To use it, first download the mfsBSD installation medium at http://mfsbsd.vx.sk (use the so-called *special edition* because it contains the installation packages). Make sure you end up with an image named ``~/Downloads/mfsbsd-se-10.1-RELEASE-amd64.iso``.

Then::

    ploy start nanobuild-vbox
    ploy bootstrap
    ploy configure nanobuild