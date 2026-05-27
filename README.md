# Migration guide to systemd from system V

To start follow this [guide](https://ericlinsechs.github.io/2024-02-26-Build-Linux-Distribution-for-NXP-iMX-8-with-Yocto-Project/):

It covers downloading repo (git tool), downloading the nxp reposioiry and building your first image.

The default settings is for this image to be build with Systemd. Our first step is change this to system V and use systemd on top.

# After following the guide
Assuming you have already built an image, open the file `build/conf/local.conf`

Add this code to the bottom of that file:
```
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
``` 

Now all that is left is to flash your hardware
