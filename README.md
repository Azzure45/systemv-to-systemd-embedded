# Migration guide to systemd from system V

To start follow this guide:
https://ericlinsechs.github.io/2024-02-26-Build-Linux-Distribution-for-NXP-iMX-8-with-Yocto-Project/

It includes downloading repo (git tool) and downloading the nxp reposioiry and building your first image.

Now the default settings are to build with Systemd. First to show a migration we have to change to system V and then back to systemd while using the system V arhiteture.

Assuming you have already built an image, open the file build/conf/local.conf

Add this code to the bottom of that file:
´
DISTRO_FEATURES:append = " systemd sysvinit"
VIRTUAL-RUNTIME_init_manager = "systemd"
VIRTUAL-RUNTIME_initscripts = "initscripts"
DISTRO_FEATURES_BACKFILL_CONSIDERED += "sysvinit"

IMAGE_INSTALL:append = " \
    systemd \
    systemdanalyze \
    systemd-compat-units \
    initscripts \
    sysvinit-inittab \
    util-linux-agetty \
    procps \
"
´
