# Linux-on-Lenovo-A10
Notes and Process for getting Linux installed on Lenovo A10 Android Laptop

## Sources
https://github.com/steffen-g/lenovo-a10

https://github.com/durandmiller/lenovo-a10

# Installation Summary
Installing linux on the laptop will use the instructions provided by steffen-g. The process requires two USB drives.

| Kernel Type       | Name of File          | Link to Kernel Image   |
| -------------     |---------------------- | ---------------------- |
| Boot from USB     | boot-sda1-init-sh.img |  http://gsg-elektronik.de/download/a10/boot-sda1-init-sh.img |
| Normal Boot       | boot-sda1-normal.img  |  http://gsg-elektronik.de/download/a10/boot-sda1-normal.img |

At a high level the first image "Boot From USB" (using boot-sda1-normal.img) will allow you to boot to an init environment allowing you to install / copy filestyem.


# Install Instructions for Booting from NAND Memory on the Device

## Prepare a Debootstrap USB stick
Create a USB stick with a rootfs of your favorite distribution. This example is for Debian but it should work the same way for Ubuntu:

### Create a rootfs USB stick
Anyone who has a Debian-based system can simply install apt-get debootstrap. Then partition any USB stick and then format it with ext3 or ext4.
All commands are executed as root.

#### Step 1: Mount USB (replace sdX with the appropriate device [you can use dmesg or df to figure this out]):
Mount /dev/sdX1 /mnt

#### Step 2: Create Debootstrap files on the USB key (ie. that's now mounted on /mnt) (you can also add other packages here) (this debootstrap assumes Debian Stretch):

```shell
sudo debootstrap --foreign --arch = armhf --include =dhcpcd5, module-init-tools, Udev, netbase, ifupdown, iproute, openssh-server, iputils-ping, wget, Net-tools, ntpdate, vim, usbutils, build-essential, Hdparm, wireless-tools, wpasupplicant, surf, inkscape, handbrake, arduino, openssh-client, ipython, ipython3, chromium, apt, git, automake, autoconf, pkg-config, libcurl4-openssl-dev, libjansson-dev, libssl-dev, libgmp-dev, g++, screen, legit, ledger, calcurse, aria2, cmus, mc, mutt, mpd, htop, task, lftp, woof, finch, links, elinks, w3m, bastet, freesweep, dtrx, rename, renameutils, tree, lfm, moc, mpg123, mps-youtube, feh, zathura, qalculate, tpp, bash, zsh, multitail, jed, wordgrinder, figlet, toilet, grc, python, python3, python3-flask, python3-django, python3-bottle, python3-scipy, python3-matplotlib, python3-pandas, python3-sql, python3-sqlparse, python3-sqlalchemy, python3-jsonpickle, python3-jsonschema, python3-jsmin, python3-pil, sqlite3, ninvaders, pacman4console, nsnake, greed, bsdgames, moon-buggy, libncurses5-dev, libsdl2-dev, robotfindskitten, zangband, gnuchess, adwaita-icon-theme, alsa-base, aspell, aspell-en, bind9-host, binutils, blt, bzip2, claws-mail-i18n, coinor-libcbc3, coinor-libcgl1, coinor-libclp1, coinor-libcoinmp1, coinor-libcoinutils3, coinor-libosi1, console-setup-linux, cpp, cpp-4.9, cryptsetup-bin, cups-bsd, cups-client, cups-common, dbus, dbus-x11, dc, dconf-gsettings-backend, dconf-service, debian-reference-common, dh-python, dictionaries-common, dpkg-dev, eject, emacsen-common, epiphany-browser-data, esound-common, fakeroot, file, fontconfig, fontconfig-config, fonts-dejavu-core, fonts-dejavu-extra, fonts-freefont-ttf, fonts-opensymbol, fonts-roboto, freepats, fuse, g++, g++-4.9, gcc, gcc-4.9, gconf-service, gconf2, gconf2-common, gdbserver, gdebi-core, geoip-database, gettext-base, giblib1, gir1.2-atk-1.0, gir1.2-freedesktop, gir1.2-gdkpixbuf-2.0, gir1.2-glib-2.0, gir1.2-gmenu-3.0, gir1.2-gtk-3.0, gir1.2-pango-1.0, git, git-man, glib-networking, glib-networking-common, glib-networking-services, gnome-desktop3-data, gnome-icon-theme-symbolic, gnome-menus, gnome-themes-standard, gnupg-agent, gnupg2, gsettings-desktop-schemas, gsfonts, gsfonts-x11, gstreamer0.10-alsa, gstreamer0.10-plugins-base, gtk2-engines-pixbuf, gvfs, gvfs-common, gvfs-daemons, gvfs-libs, hdparm, hicolor-icon-theme, idle-python2.7, idle-python3.4, iso-codes, iw, jackd, jackd2, javascript-common, kbd, krb5-locales, libaa1, libabw-0.1-1, libalgorithm-c3-perl, libalgorithm-diff-perl, libalgorithm-diff-xs-perl, libalgorithm-merge-perl, libarchive-extract-perl, libarchive13, libasan1, libasn1-8-heimdal, libasound2, libasound2-data, libaspell15, libasprintf0c2, libass5, libassuan0, libasyncns0, libatasmart4, libatk-bridge2.0-0, libatk1.0-0, libatk1.0-data, libatomic1, libatspi2.0-0, libaudio2, libaudiofile1, libavahi-client3, libavahi-common-data, libavahi-common3, libavahi-core7, libavahi-glib1, libavahi-gobject0, libavc1394-0, libavcodec56, libavformat56, libavresample2, libavutil54, libbind9-90, libblas-common, libblas3, libbluetooth3, libbluray1, libboost-atomic1.55.0, libboost-date-time1.55.0, libboost-filesystem1.55.0, libboost-program-options1.55.0, libboost-regex1.55.0, libboost-system1.55.0, libboost-thread1.55.0, libc-ares2, libc-dev-bin, libc6-dbg, libc6-dev, libcaca0, libcairo-gobject2, libcairo2, libcanberra-gtk3-0, libcanberra0, libcap-ng0, libcdio-cdda1, libcdio-paranoia1, libcdio13, libcdparanoia0, libcdr-0.1-1, libcgi-fast-perl, libcgi-pm-perl, libchromaprint0, libclass-c3-perl, libclass-c3-xs-perl, libcloog-isl4, libclucene-contribs1, libclucene-core1, libcmis-0.4-4, libcolamd2.8.0, libcolord2, libcompfaceg1, libcpan-meta-perl, libcroco3, libcups2, libcupsfilters1, libcupsimage2, libcurl3, libcurl3-gnutls, libcwiid1, libdaemon0, libdata-optlist-perl, libdata-section-perl, libdatrie1, libdbus-glib-1-2, libdc1394-22, libdca0, libdconf1, libdevmapper-event1.02.1, libdirectfb-1.2-9, libdns100, libdpkg-perl, libdrm-nouveau2, libdrm-radeon1, libdv4, libdvdnav4, libdvdread4, libe-book-0.1-1, libedit2, libegl1-mesa, libelf1, libelfg0, libenca0, libenchant1c2a, libeot0, libepoxy0, liberror-perl, libesd0, libetonyek-0.1-1, libetpan17, libevdev2, libevent-2.0-5, libexif12, libexpat1, libexpat1-dev, libexttextcat-2.0-0, libexttextcat-data, libfaad2, libfakeroot, libfcgi-perl, libfftw3-double3, libfftw3-single3, libfile-fcntllock-perl, libflac8, libflite1, libfltk1.3, libfluidsynth1, libfm-data, libfm-extra4, libfm-gtk-data, libfm-gtk4, libfm-modules, libfm4, libfontconfig1, libfontenc1, libfreehand-0.1-1, libfreetype6, libfribidi0, libfuse2, libgbm1, libgcc-4.9-dev, libgconf-2-4, libgd3, libgdk-pixbuf2.0-0, libgdk-pixbuf2.0-common, libgeoclue0, libgeoip1, libgfortran3, libgif4, libgirepository-1.0-1, libgksu2-0, libgl1-mesa-glx, libglapi-mesa, libglew1.10, libglib2.0-0, libglib2.0-bin, libglib2.0-data, libgltf-0.0-0, libglu1-mesa, libgme0, libgnome-desktop-3-10, libgnome-keyring-common, libgnome-keyring0, libgnome-menu-3-0, libgoa-1.0-0b, libgoa-1.0-common, libgomp1, libgpgme11, libgphoto2-6, libgphoto2-port10, libgpm2, libgraphite2-3, libgsm1, libgssapi-krb5-2, libgssapi3-heimdal, libgstreamer-plugins-bad1.0-0, libgstreamer-plugins-base0.10-0, libgstreamer-plugins-base1.0-0, libgstreamer0.10-0, libgstreamer1.0-0, libgtk-3-0, libgtk-3-bin, libgtk-3-common, libgtk2.0-0, libgtk2.0-bin, libgtk2.0-common, libgtkglext1, libgtop2-7, libgtop2-common, libgudev-1.0-0, libharfbuzz-icu0, libharfbuzz0b, libhcrypto4-heimdal, libheimbase1-heimdal, libheimntlm0-heimdal, libhsqldb1.8.0-java, libhunspell-1.3-0, libhx509-5-heimdal, libhyphen0, libice6, libid3tag0, libiec61883-0, libilmbase6, libimlib2, libimobiledevice4, libisc95, libisccc90, libisccfg90, libisl10, libiw30, libjack-jackd2-0, libjasper1, libjavascriptcoregtk-3.0-0, libjbig0, libjpeg62-turbo, libjs-jquery, libjs-prettify, libjson-glib-1.0-0, libjson-glib-1.0-common, libk5crypto3, libkate1, libkeyutils1, libkrb5-26-heimdal, libkrb5-3, libkrb5support0, libksba8, liblangtag-common, liblangtag1, liblapack3, liblcms2-2, libldap-2.4-2, libldb1, liblightdm-gobject-1-0, liblockfile-bin, liblockfile1, liblog-message-perl, liblog-message-simple-perl, libltdl7, libluajit-5.1-common, liblvm2app2.2, liblwres90, liblzo2-2, libmad0, libmagic1, libmenu-cache-bin, libmenu-cache3, libmhash2, libmikmod3, libmimic0, libmjpegutils-2.1-0, libmms0, libmng1, libmodplug1, libmodule-build-perl, libmodule-pluggable-perl, libmodule-signature-perl, libmotif-common, libmozjs185-1.0, libmp3lame0, libmpc3, libmpdec2, libmpeg2encpp-2.1-0, libmpfr4, libmpg123-0, libmplex2-2.1-0, libmro-compat-perl, libmspub-0.1-1, libmtdev1, libmtp-common, libmtp9, libmwaw-0.3-3, libmythes-1.2-0, libneon27-gnutls, libnfsidmap2, libnl-3-200, libnl-genl-3-200, libnotify4, libnspr4, libnss-mdns, libnss3, libntdb1, libobrender29, libobt2, libodfgen-0.1-1, libofa0, libogg0, libopenal-data, libopenal1, libopencv-calib3d2.4, libopencv-contrib2.4, libopencv-core2.4, libopencv-features2d2.4, libopencv-flann2.4, libopencv-highgui2.4, libopencv-imgproc2.4, libopencv-legacy2.4, libopencv-ml2.4, libopencv-objdetect2.4, libopencv-video2.4, libopenexr6, libopenjpeg5, libopts25, libopus0, liborc-0.4-0, liborcus-0.8-0, libpackage-constants-perl, libpackagekit-glib2-18, libpam-systemd, libpango-1.0-0, libpango1.0-0, libpangocairo-1.0-0, libpangoft2-1.0-0, libpangox-1.0-0, libpangoxft-1.0-0, libparams-util-perl, libparted2, libpciaccess0, libpcsclite1, libpisock9, libpixman-1-0, libplist2, libpng12-dev, libpod-latex-perl, libpod-readme-perl, libpolkit-agent-1-0, libpolkit-backend-1-0, libpolkit-gobject-1-0, libpoppler46, libportaudio2, libportmidi0, libproxy1, libpth20, libpulse0, libpython-stdlib, libpython2.7, libpython2.7-minimal, libpython2.7-stdlib, libpython3-dev, libpython3-stdlib, , libqscintilla2-11, libqscintilla2-l10n, libqt4-dbus, libqt4-network, libqt4-xml, libqt4-xmlpatterns, libqtcore4, libqtdbus4, libqtgui4, libqtwebkit4, libraptor2-0, librasqal3, libraw1394-11, librdf0, libregexp-common-perl, libreoffice-base-core, libreoffice-base-drivers, libreoffice-common, libreoffice-core, libreoffice-style-galaxy, librest-0.7-0, librevenge-0.0-0, libroken18-heimdal, librsvg2-2, librsvg2-common, , librtmp1, libruby2.1, libsamplerate0, libsasl2-2, libsasl2-modules, libsasl2-modules-db, libsbc1, libschroedinger-1.0-0, libscsynth1, libsdl-image1.2, libsdl-mixer1.2, libsdl-ttf2.0-0, libsdl1.2debian, libsecret-1-0, libsecret-common, libsgutils2-2, libshout3, libsm6, libsmbclient, libsndfile1, libsoftware-license-perl, libsoundtouch0, libsoup-gnome2.4-1, libsoup2.4-1, libspandsp2, libspeex1, libsrtp0, libssh-4, libssh2-1, libstartup-notification0, libstdc++-4.9-dev, libsub-exporter-perl, libsub-install-perl, libswscale3, libtag1-vanilla, libtag1c2a, libtalloc2, libtcl8.5, libtcl8.6, libterm-ui-perl, libtevent0, libtext-soundex-perl, libtext-template-perl, libthai-data, libthai0, libtheora0, libtiff5, libtimedate-perl, libtirpc1, libtk8.5, libtk8.6, libtxc-dxtn-s2tc0, libubsan0, libudisks2-0, libusb-1.0-0, libusbmuxd2, libv4l-0, libv4l2rds0, libv4lconvert0, libv8-3.14.5, libva1, libvdpau1, libvisio-0.1-1, libvisual-0.4-0, libvisual-0.4-plugins, libvo-aacenc0, libvo-amrwbenc0, libvorbis0a, libvorbisenc2, libvorbisfile3, libvpx1, libvte-common, libvte9, libwavpack1, libwayland-client0, libwayland-cursor0, libwayland-server0, libwbclient0, libwebkitgtk-3.0-0, libwebkitgtk-3.0-common, libwebp5, libwebpdemux1, libwebpmux1, libwildmidi-config, libwildmidi1, libwind0-heimdal, libwnck-3-0, libwnck-3-common, libwnck-common, libwnck22, libwpd-0.10-10, libwpg-0.3-3, libwps-0.3-3, libwrap0, libx11-6, libx11-data, libx11-xcb1, libx264-142, libxau6, libxaw7, libxcb-dri2-0, libxcb-dri3-0, libxcb-glx0, libxcb-present0, libxcb-render0, libxcb-shape0, libxcb-shm0, libxcb-sync1, libxcb-util0, libxcb-xfixes0, libxcb1, libxcomposite1, libxcursor1, libxdamage1, libxdmcp6, libxext6, libxfce4ui-1-0, libxfce4util-bin, libxfce4util-common, libxfce4util6, libxfconf-0-2, libxfixes3, libxfont1, libxft2, libxi6, libxinerama1, libxkbcommon0, libxkbfile1, libxklavier16, libxm4, libxml2, libxmu6, libxmuu1, libxpm4, libxrandr2, libxrender1, libxres1, libxshmfence1, libxslt1.1, libxss1, libxt6, libxtst6, libxv1, libxvidcore4, libxxf86dga1, libxxf86vm1, libyajl2, libyaml-0-2, libzbar0, lightdm-gtk-greeter, linux-libc-dev, lp-solve, lsb-release, lxmenu-data, lxpanel-data, lxsession, make, mime-support, ncurses-term, netsurf-common, nodejs, nodejs-legacy, ntfs-3g, openssh-client, openssh-server, openssh-sftp-server, openssl, packagekit, patch, perl, perl-modules, poppler-data, poppler-utils, powermgmt-base, python-apt-common, python-cairo, python-chardet, python-colorama, python-dbus, python-dbus-dev, python-distlib, python-gi, python-gobject, python-gobject-2, python-gtk2, python-html5lib, python-minimal, python-ndg-httpsclient, python-numpy, python-openssl, python-pil, python-pkg-resources, python-pyasn1, python-requests, python-setuptools, python-six, python-support, python-talloc, python-urllib3, python-wheel, python2.7, python2.7-minimal, python3-apt, python3-chardet, python3-colorama, python3-debian, python3-dev, python3-distlib, python3-html5lib, python3-minimal, python3-pil, python3-pkg-resources, python3-requests, python3-setuptools, python3-six, python3-urllib3, python3-wheel, qdbus, qjackctl, qtchooser, qtcore4-l10n, rename, rpcbind, rsync, ruby, ruby2.1, rubygems-integration, samba-common, samba-libs, scrot, sgml-base, shared-mime-info, squeak-plugins-scratch, squeak-vm, supercollider, supercollider-common, supercollider-ide, supercollider-language, supercollider-server, supercollider-supernova, tcl8.5, tcpd, tk8.5, tk8.6-blt2.5, triggerhappy, ucf, udisks2, uno-libs3, ure, va-driver-all, vdpau-va-driver, wireless-regdb, x11-common, x11-utils, x11-xkb-utils, x11-xserver-utils, xauth, xdg-user-dirs, xfce-keyboard-shortcuts, xfconf, xfonts-100dpi, xfonts-encodings, xfonts-utils, xkb-data, xml-core, xserver-common, xserver-xorg-core, xserver-xorg-input-all, xserver-xorg-input-evdev, xserver-xorg-input-synaptics, zenity-common, zlib1g-dev, acl, adduser, alacarte, alsa-utils, apt, apt-utils, aptitude, aptitude-common, avahi-daemon, base-files, base-passwd, bash, bash-completion, bsdmainutils, bsdutils, build-essential, ca-certificates, cifs-utils, claws-mail, console-setup, coreutils, cpio, crda, cron, curl, dash, debconf, debconf-i18n, debconf-utils, debian-reference-en, debianutils, desktop-base, desktop-file-utils, dhcpcd5, diffutils, dillo, dmidecode, dmsetup, dosfstools, dphys-swapfile, dpkg, e2fslibs, e2fsprogs, ed, epiphany-browser, fake-hwclock, fbset, findutils, firmware-atheros, firmware-brcm80211, firmware-libertas, firmware-ralink, firmware-realtek, fonts-dejavu, fonts-sil-gentium-basic, galculator, gcc-4.9-base, gdb, git-core, gksu, gnome-icon-theme, gnome-themes-standard-data, gnupg, gpgv, gpicview, , grep, groff-base, gstreamer1.0-alsa, gstreamer1.0-libav, gstreamer1.0-plugins-bad, gstreamer1.0-plugins-base, gstreamer1.0-plugins-good, gstreamer1.0-x, gtk2-engines, gvfs-backends, gvfs-fuse, gzip, hardlink, hostname, idle, idle3, ifupdown, info, init, init-system-helpers, initramfs-tools, initscripts, insserv, install-info, iproute2, iptables, iputils-ping, isc-dhcp-client, isc-dhcp-common, java-common, keyboard-configuration, klibc-utils, kmod, leafpad, less, libacl1, libapt-inst1.5, libapt-pkg4.12, libattr1, libaudit-common, libaudit1, libblkid1, libbsd0, libbz2-1.0, libc-bin, libc6, libcap2, libcap2-bin, libcomerr2, libcryptsetup4, libcwidget3, libdb5.3, libdbus-1-3, libdebconfclient0, libdevmapper1.02.1, libdns-export100, libdrm2, libestr0, libffi6, libfreetype6-dev, libgcc1, libgcrypt20, libgdbm3, libgl1-mesa-dri, libgles1-mesa, libgles2-mesa, libgmp10, libgnutls-deb0-28, libgnutls-openssl27, libgpg-error0, libhogweed2, libicu52, libident, libidn11, libirs-export91, libisc-export95, libisccfg-export90, libjson-c2, libklibc, libkmod2, liblocale-gettext-perl, liblogging-stdlog0, liblognorm1, liblzma5, libmount1, libncurses5, libncursesw5, libnettle4, libnewt0.52, libnfnetlink0, libnih-dbus1, libnih1, libp11-kit0, libpam-modules, libpam-modules-bin, libpam-runtime, libpam0g, libpcre3, libpipeline1, libpng12-0, libpopt0, libprocps3, libpsl0, libreadline6, libreoffice, libreoffice-avmedia-backend-gstreamer, libreoffice-base, libreoffice-calc, libreoffice-draw, libreoffice-gtk, libreoffice-impress, libreoffice-java-common, libreoffice-math, libreoffice-report-builder-bin, libreoffice-sdbc-hsqldb, libreoffice-writer, libselinux1, libsemanage-common, libsemanage1, libsepol1, libservlet2.5-java, libsigc++-1.2-5c2, libsigc++-2.0-0c2a, libslang2, libsmartcols1, libsqlite3-0, libss2, libssl1.0.0, libstdc++6, libsysfs2, libsystemd0, libtasn1-6, libtext-charwidth-perl, libtext-iconv-perl, libtext-wrapi18n-perl, libtinfo5, libudev1, libusb-0.1-4, libustr-1.0-1, libuuid1, libxapian22, libxtables10, lightdm, locales, login, logrotate, lsb-base, lua5.1, luajit, lxappearance, lxappearance-obconf, lxde, lxde-common, lxde-core, lxde-icon-theme, lxinput, lxpanel, lxrandr, lxtask, lxterminal, makedev, man-db, manpages, manpages-dev, mawk, menu-xdg, module-init-tools, mount, mountall, multiarch-support, nano, ncdu, ncurses-base, ncurses-bin, net-tools, netbase, netcat-openbsd, netcat-traditional, netsurf-gtk, nfs-common, ntp, openbox, , parted, passwd, pcmanfm, perl-base, pkg-config, plymouth, policykit-1, procps, psmisc, , python-pygame, python-serial, python-tk, python3, , python3-numpy, python3-pip, python3-serial, python3-tk, python3-uno, readline-common, rsyslog, scratch, sed, sensible-utils, ssh, startpar, strace, sudo, systemd, systemd-sysv, sysv-rc, sysvinit-utils, tar, tasksel, tasksel-data, timidity, traceroute, tree, tzdata, udev, udisks, unzip, usbutils, util-linux, v4l-utils, vim-common, vim-tiny, wget, whiptail, wireless-tools, wpasupplicant, x2x, xarchiver, xcompmgr, xdg-utils, xinit, xpdf, xserver-xorg, xserver-xorg-video-fbdev, xz-utils, zenity, zlib1g --variant = minbase stretch /mnt http://ftp.de.debian.org/debian
```


#### Step 3: Preparing to flash special Kernel files on the Lenovo Ideapad A10 laptop

There is a kernel that must be used to allow boot from USB: boot-sda1-init-sh.img http://gsg-elektronik.de/download/a10/boot-sda1-init-sh.img
This is an Android bootimage consisting of kernel and initrd.

##### Flashing the "Boot from USB" kernel

1. First download the flashtool from here ( https://github.com/steffen-g/lenovo-a10/tree/master/rkflashtool-5.1-src ) and compile. [You can use the GitHub instructions for the same tool]

2. Plug in the Lenovo laptop to your main linux machine and make the laptop go into bootloader mode by physically bridging of the pads and pressing the power button (or alternatively press and hold the powerbutton while also press the magnifying glass button and" R "when you turn on, if you use dmesg in the terminal of your main linux machine the Lenovo with will appear with USB ID 2207: 310b.)(or if in android run the "adb reboot bootloader" in the terminal while the laptop is in developer mode while running android).

3. Flash the first "boot from usb" img from your main linux machine: boot-sda1-init-sh.img http://gsg-elektronik.de/download/a10/boot-sda1-init-sh.img:

```shell
$ sudo ./rkflashtool-5.1-src/rkflashtool w 0x008000 0x00008000 < boot-sda1-init-sh.img
```

4. You will see the following in the terminal
```shell
$ rkflashtool: fatal: premature end-of-file reached.
```

5. Plug in the usb key with the debootstrap files and reset the lenovo laptop.

If the reset completes successfully, the lenovo laptop should now boot into an unfinished Debian statea and the screen will display

```shell
#
```

6. Finish debootstrap process on the lenovo A10 laptop:
```shell
cd /debootstrap
mount -o remount,rw /
```

this will mount the usb with the debootstrap files and the command prompt will state
```shell
[] EXT4-fs (sdX1): re-mounted. Opts: barrier=1,data=ordered
```

7.  type in the following:
```shell
./debootstrap --second-stage

command line prompt will display:
```shell
Install core packages...
```
and the rest of the linux installation will proceed

8. type passwd in the shell prompt:
```shell
passwd
```
to set your password

9. Wait until that above processes complete.

10. Reboot the laptop (hold power + magnifying glass and "R" button. Flash this kernel from your main linux machine: boot-sda1-normal.img http://gsg-elektronik.de/download/a10/boot-sda1-normal.img
sudo ./rkflashtool-5.1-src/rkflashtool w 0x008000 0x00008000 < boot-sda1-normal.img

11. After a reset, the device will boot into a complete Debian installation from USB stick. At this point, you can set up WLAN with wpa_supplicant, if you want Xorg and a window manager.


# Install Instructions for Booting from USB

## Prepare a Debootstrap USB stick
Create a USB stick with a rootfs of your favorite distribution. This example is for Debian but it should work the same way for Ubuntu:

### Create a rootfs USB stick
Anyone who has a Debian-based system can simply install apt-get debootstrap. Then partition any USB stick and then format it with ext3 or ext4.
All commands are executed as root.

#### Step 1: Mount USB (replace sdX with the appropriate device [you can use dmesg or df to figure this out]):
Mount /dev/sdX1 /mnt

#### Step 2: Create Debootstrap files on the USB key (ie. that's now mounted on /mnt) (you can also add other packages here) (this debootstrap assumes Debian Stretch):

Debootstrap --foreign --arch = armhf --include = module-init-tools,
Udev, netbase, ifupdown, iproute, openssh-server, dhcpcd, iputils-ping, wget,
Net-tools, ntpdate, uboot-mkimage, uboot-envtools, vim, usbutils, build-essential,
Hdparm, wireless-tools, wpasupplicant --variant = minbase stretch /mnt
Http://ftp.de.debian.org/debian


#### Step 3: Preparing to flash special Kernel files on the Lenovo Ideapad A10 laptop

There is a kernel that must be used to allow boot from USB: boot-sda1-init-sh.img http://gsg-elektronik.de/download/a10/boot-sda1-init-sh.img
This is an Android bootimage consisting of kernel and initrd.

##### Flashing the "Boot from USB" kernel

1. First download the flashtool from here ( https://github.com/steffen-g/lenovo-a10/tree/master/rkflashtool-5.1-src ) and compile. [You can use the GitHub instructions for the same tool]

2. Plug in the Lenovo laptop to your main linux machine and make the laptop go into bootloader mode by physically bridging of the pads and pressing the power button (or alternatively press and hold the powerbutton while also press the magnifying glass button and" R "when you turn on, if you use dmesg in the terminal of your main linux machine the Lenovo with will appear with USB ID 2207: 310b.)(or if in android run the "adb reboot bootloader" in the terminal while the laptop is in developer mode while running android).

3. Flash the first boot from usb img from your main linux machine: boot-sda1-init-sh.img http://gsg-elektronik.de/download/a10/boot-sda1-init-sh.img:

```shell
$ sudo ./rkflashtool-5.1-src/rkflashtool w 0x008000 0x00008000 < boot-sda1-init-sh.img
```

4. You will see the following in the terminal
```shell
$ rkflashtool: fatal: premature end-of-file reached.
```

5. Plug in the usb key with the debootstrap files and reset the lenovo laptop.

If the reset completes successfully, the lenovo laptop should now boot into an unfinished Debian statea and the screen will display

```shell
#
```

6. Finish debootstrap process on the lenovo A10 laptop:
```shell
cd /debootstrap
mount -o remount,rw /
```

this will mount the usb with the debootstrap files and the command prompt will state
```shell
[] EXT4-fs (sdX1): re-mounted. Opts: barrier=1,data=ordered
```

7.  type in the following:
```shell
./debootstrap --second-stage

command line prompt will display:
```shell
Install core packages...
```
and the rest of the linux installation will proceed

8. type passwd in the shell prompt:
```shell
passwd
```
to set your password

9. Wait until that above processes complete.

10. Reboot the laptop (hold power + magnifying glass and "R" button. Flash this kernel from your main linux machine: boot-sda1-normal.img http://gsg-elektronik.de/download/a10/boot-sda1-normal.img
sudo ./rkflashtool-5.1-src/rkflashtool w 0x008000 0x00008000 < boot-sda1-normal.img

11. After a reset, the device will boot into a complete Debian installation from USB stick. At this point, you can set up WLAN with wpa_supplicant, if you want Xorg and a window manager.
[I don't think I've the wpa supplicant steps correct, when I tried it caused my laptop to crash]


##### Connect to wifi via wpa_supplicant

Create a config file in /etc/wpa_supplicant.conf

Example:
```shell
network={
    ssid="ssid_name"
    psk="password"
}
```

Run WPA Supplicant
```shell
wpa_supplicant -B -iwlan0 -c/etc/wpa_supplicant.conf -Dwext
```

Run
```shell
dhcpcd wlan0
or dhclient -r
dhclient wlan0
```

## Packages from APT (need to be installed prior to trying debootstrap)

First try to install the following
```shell
sudo apt-get install dhcpcd5 module-init-tools  
```
sudo apt-get install  uboot-mkimage uboot-envtools

Then try to install:
```shell
sudo apt-get install debootstrap Udev netbase ifupdown iproute openssh-server iputils-ping wget Net-tools ntpdate  vim usbutils build-essential Hdparm wireless-tools wpasupplicant surf inkscape handbrake arduino openssh-client ipython ipython3 chromium apt git automake autoconf pkg-config libcurl4-openssl-dev libjansson-dev libssl-dev libgmp-dev g++ screen legit ledger calcurse aria2 cmus mc mutt mpd htop task lftp woof finch links elinks w3m bastet freesweep dtrx rename renameutils tree lfm moc mpg123 mps-youtube feh zathura qalculate tpp bash zsh multitail jed wordgrinder figlet toilet grc python python3 python3-flask python3-django python3-bottle python3-scipy python3-matplotlib python3-pandas python3-sql python3-sqlparse python3-sqlalchemy python3-jsonpickle python3-jsonschema python3-jsmin python3-pil sqlite3 ninvaders pacman4console nsnake greed bsdgames moon-buggy libncurses5-dev libsdl2-dev robotfindskitten zangband gnuchess adwaita-icon-theme alsa-base aspell aspell-en bind9-host binutils blt bzip2 claws-mail-i18n coinor-libcbc3 coinor-libcgl1 coinor-libclp1 coinor-libcoinmp1 coinor-libcoinutils3 coinor-libosi1 console-setup-linux cpp cpp-4.9 cryptsetup-bin cups-bsd cups-client cups-common dbus dbus-x11 dc dconf-gsettings-backend dconf-service debian-reference-common dh-python dictionaries-common dpkg-dev eject emacsen-common epiphany-browser-data esound-common fakeroot file fontconfig fontconfig-config fonts-dejavu-core fonts-dejavu-extra fonts-freefont-ttf fonts-opensymbol fonts-roboto freepats fuse g++ g++-4.9 gcc gcc-4.9 gconf-service gconf2 gconf2-common gdbserver gdebi-core geoip-database gettext-base giblib1 gir1.2-atk-1.0 gir1.2-freedesktop gir1.2-gdkpixbuf-2.0 gir1.2-glib-2.0 gir1.2-gmenu-3.0 gir1.2-gtk-3.0 gir1.2-pango-1.0 git git-man glib-networking glib-networking-common glib-networking-services gnome-desktop3-data gnome-icon-theme-symbolic gnome-menus gnome-themes-standard gnupg-agent gnupg2 gsettings-desktop-schemas gsfonts gsfonts-x11 gstreamer0.10-alsa gstreamer0.10-plugins-base gtk2-engines-pixbuf gvfs gvfs-common gvfs-daemons gvfs-libs hdparm hicolor-icon-theme idle-python2.7 idle-python3.4 iso-codes iw jackd jackd2 javascript-common kbd krb5-locales libaa1 libabw-0.1-1 libalgorithm-c3-perl libalgorithm-diff-perl libalgorithm-diff-xs-perl libalgorithm-merge-perl libarchive-extract-perl libarchive13 libasan1 libasn1-8-heimdal libasound2 libasound2-data libaspell15 libasprintf0c2 libass5 libassuan0 libasyncns0 libatasmart4 libatk-bridge2.0-0 libatk1.0-0 libatk1.0-data libatomic1 libatspi2.0-0 libaudio2 libaudiofile1 libavahi-client3 libavahi-common-data libavahi-common3 libavahi-core7 libavahi-glib1 libavahi-gobject0 libavc1394-0 libavcodec56 libavformat56 libavresample2 libavutil54 libbind9-90 libblas-common libblas3 libbluetooth3 libbluray1 libboost-atomic1.55.0 libboost-date-time1.55.0 libboost-filesystem1.55.0 libboost-program-options1.55.0 libboost-regex1.55.0 libboost-system1.55.0 libboost-thread1.55.0 libc-ares2 libc-dev-bin libc6-dbg libc6-dev libcaca0 libcairo-gobject2 libcairo2 libcanberra-gtk3-0 libcanberra0 libcap-ng0 libcdio-cdda1 libcdio-paranoia1 libcdio13 libcdparanoia0 libcdr-0.1-1 libcgi-fast-perl libcgi-pm-perl libchromaprint0 libclass-c3-perl libclass-c3-xs-perl libcloog-isl4 libclucene-contribs1 libclucene-core1 libcmis-0.4-4 libcolamd2.8.0 libcolord2 libcompfaceg1 libcpan-meta-perl libcroco3 libcups2 libcupsfilters1 libcupsimage2 libcurl3 libcurl3-gnutls libcwiid1 libdaemon0 libdata-optlist-perl libdata-section-perl libdatrie1 libdbus-glib-1-2 libdc1394-22 libdca0 libdconf1 libdevmapper-event1.02.1 libdirectfb-1.2-9 libdns100 libdpkg-perl libdrm-nouveau2 libdrm-radeon1 libdv4 libdvdnav4 libdvdread4 libe-book-0.1-1 libedit2 libegl1-mesa libelf1 libelfg0 libenca0 libenchant1c2a libeot0 libepoxy0 liberror-perl libesd0 libetonyek-0.1-1 libetpan17 libevdev2 libevent-2.0-5 libexif12 libexpat1 libexpat1-dev libexttextcat-2.0-0 libexttextcat-data libfaad2 libfakeroot libfcgi-perl libfftw3-double3 libfftw3-single3 libfile-fcntllock-perl libflac8 libflite1 libfltk1.3 libfluidsynth1 libfm-data libfm-extra4 libfm-gtk-data libfm-gtk4 libfm-modules libfm4 libfontconfig1 libfontenc1 libfreehand-0.1-1 libfreetype6 libfribidi0 libfuse2 libgbm1 libgcc-4.9-dev libgconf-2-4 libgd3 libgdk-pixbuf2.0-0 libgdk-pixbuf2.0-common libgeoclue0 libgeoip1 libgfortran3 libgif4 libgirepository-1.0-1 libgksu2-0 libgl1-mesa-glx libglapi-mesa libglew1.10 libglib2.0-0 libglib2.0-bin libglib2.0-data libgltf-0.0-0 libglu1-mesa libgme0 libgnome-desktop-3-10 libgnome-keyring-common libgnome-keyring0 libgnome-menu-3-0 libgoa-1.0-0b libgoa-1.0-common libgomp1 libgpgme11 libgphoto2-6 libgphoto2-port10 libgpm2 libgraphite2-3 libgsm1 libgssapi-krb5-2 libgssapi3-heimdal libgstreamer-plugins-bad1.0-0 libgstreamer-plugins-base0.10-0 libgstreamer-plugins-base1.0-0 libgstreamer0.10-0 libgstreamer1.0-0 libgtk-3-0 libgtk-3-bin libgtk-3-common libgtk2.0-0 libgtk2.0-bin libgtk2.0-common libgtkglext1 libgtop2-7 libgtop2-common libgudev-1.0-0 libharfbuzz-icu0 libharfbuzz0b libhcrypto4-heimdal libheimbase1-heimdal libheimntlm0-heimdal libhsqldb1.8.0-java libhunspell-1.3-0 libhx509-5-heimdal libhyphen0 libice6 libid3tag0 libiec61883-0 libilmbase6 libimlib2 libimobiledevice4 libisc95 libisccc90 libisccfg90 libisl10 libiw30 libjack-jackd2-0 libjasper1 libjavascriptcoregtk-3.0-0 libjbig0 libjpeg62-turbo libjs-jquery libjs-prettify libjson-glib-1.0-0 libjson-glib-1.0-common libk5crypto3 libkate1 libkeyutils1 libkrb5-26-heimdal libkrb5-3 libkrb5support0 libksba8 liblangtag-common liblangtag1 liblapack3 liblcms2-2 libldap-2.4-2 libldb1 liblightdm-gobject-1-0 liblockfile-bin liblockfile1 liblog-message-perl liblog-message-simple-perl libltdl7 libluajit-5.1-common liblvm2app2.2 liblwres90 liblzo2-2 libmad0 libmagic1 libmenu-cache-bin libmenu-cache3 libmhash2 libmikmod3 libmimic0 libmjpegutils-2.1-0 libmms0 libmng1 libmodplug1 libmodule-build-perl libmodule-pluggable-perl libmodule-signature-perl libmotif-common libmozjs185-1.0 libmp3lame0 libmpc3 libmpdec2 libmpeg2encpp-2.1-0 libmpfr4 libmpg123-0 libmplex2-2.1-0 libmro-compat-perl libmspub-0.1-1 libmtdev1 libmtp-common libmtp9 libmwaw-0.3-3 libmythes-1.2-0 libneon27-gnutls libnfsidmap2 libnl-3-200 libnl-genl-3-200 libnotify4 libnspr4 libnss-mdns libnss3 libntdb1 libobrender29 libobt2 libodfgen-0.1-1 libofa0 libogg0 libopenal-data libopenal1 libopencv-calib3d2.4 libopencv-contrib2.4 libopencv-core2.4 libopencv-features2d2.4 libopencv-flann2.4 libopencv-highgui2.4 libopencv-imgproc2.4 libopencv-legacy2.4 libopencv-ml2.4 libopencv-objdetect2.4 libopencv-video2.4 libopenexr6 libopenjpeg5 libopts25 libopus0 liborc-0.4-0 liborcus-0.8-0 libpackage-constants-perl libpackagekit-glib2-18 libpam-systemd libpango-1.0-0 libpango1.0-0 libpangocairo-1.0-0 libpangoft2-1.0-0 libpangox-1.0-0 libpangoxft-1.0-0 libparams-util-perl libparted2 libpciaccess0 libpcsclite1 libpisock9 libpixman-1-0 libplist2 libpng12-dev libpod-latex-perl libpod-readme-perl libpolkit-agent-1-0 libpolkit-backend-1-0 libpolkit-gobject-1-0 libpoppler46 libportaudio2 libportmidi0 libproxy1 libpth20 libpulse0 libpython-stdlib libpython2.7 libpython2.7-minimal libpython2.7-stdlib libpython3-dev libpython3-stdlib  libqscintilla2-11 libqscintilla2-l10n libqt4-dbus libqt4-network libqt4-xml libqt4-xmlpatterns libqtcore4 libqtdbus4 libqtgui4 libqtwebkit4 libraptor2-0 librasqal3 libraw1394-11 librdf0 libregexp-common-perl libreoffice-base-core libreoffice-base-drivers libreoffice-common libreoffice-core libreoffice-style-galaxy librest-0.7-0 librevenge-0.0-0 libroken18-heimdal librsvg2-2 librsvg2-common  librtmp1 libruby2.1 libsamplerate0 libsasl2-2 libsasl2-modules libsasl2-modules-db libsbc1 libschroedinger-1.0-0 libscsynth1 libsdl-image1.2 libsdl-mixer1.2 libsdl-ttf2.0-0 libsdl1.2debian libsecret-1-0 libsecret-common libsgutils2-2 libshout3 libsm6 libsmbclient libsndfile1 libsoftware-license-perl libsoundtouch0 libsoup-gnome2.4-1 libsoup2.4-1 libspandsp2 libspeex1 libsrtp0 libssh-4 libssh2-1 libstartup-notification0 libstdc++-4.9-dev libsub-exporter-perl libsub-install-perl libswscale3 libtag1-vanilla libtag1c2a libtalloc2 libtcl8.5 libtcl8.6 libterm-ui-perl libtevent0 libtext-soundex-perl libtext-template-perl libthai-data libthai0 libtheora0 libtiff5 libtimedate-perl libtirpc1 libtk8.5 libtk8.6 libtxc-dxtn-s2tc0 libubsan0 libudisks2-0 libusb-1.0-0 libusbmuxd2 libv4l-0 libv4l2rds0 libv4lconvert0 libv8-3.14.5 libva1 libvdpau1 libvisio-0.1-1 libvisual-0.4-0 libvisual-0.4-plugins libvo-aacenc0 libvo-amrwbenc0 libvorbis0a libvorbisenc2 libvorbisfile3 libvpx1 libvte-common libvte9 libwavpack1 libwayland-client0 libwayland-cursor0 libwayland-server0 libwbclient0 libwebkitgtk-3.0-0 libwebkitgtk-3.0-common libwebp5 libwebpdemux1 libwebpmux1 libwildmidi-config libwildmidi1 libwind0-heimdal libwnck-3-0 libwnck-3-common libwnck-common libwnck22 libwpd-0.10-10 libwpg-0.3-3 libwps-0.3-3 libwrap0 libx11-6 libx11-data libx11-xcb1 libx264-142 libxau6 libxaw7 libxcb-dri2-0 libxcb-dri3-0 libxcb-glx0 libxcb-present0 libxcb-render0 libxcb-shape0 libxcb-shm0 libxcb-sync1 libxcb-util0 libxcb-xfixes0 libxcb1 libxcomposite1 libxcursor1 libxdamage1 libxdmcp6 libxext6 libxfce4ui-1-0 libxfce4util-bin libxfce4util-common libxfce4util6 libxfconf-0-2 libxfixes3 libxfont1 libxft2 libxi6 libxinerama1 libxkbcommon0 libxkbfile1 libxklavier16 libxm4 libxml2 libxmu6 libxmuu1 libxpm4 libxrandr2 libxrender1 libxres1 libxshmfence1 libxslt1.1 libxss1 libxt6 libxtst6 libxv1 libxvidcore4 libxxf86dga1 libxxf86vm1 libyajl2 libyaml-0-2 libzbar0 lightdm-gtk-greeter linux-libc-dev lp-solve lsb-release lxmenu-data lxpanel-data lxsession make mime-support ncurses-term netsurf-common nodejs nodejs-legacy ntfs-3g openssh-client openssh-server openssh-sftp-server openssl packagekit patch perl perl-modules poppler-data poppler-utils powermgmt-base python-apt-common python-cairo python-chardet python-colorama python-dbus python-dbus-dev python-distlib python-gi python-gobject python-gobject-2 python-gtk2 python-html5lib python-minimal python-ndg-httpsclient python-numpy python-openssl python-pil python-pkg-resources python-pyasn1 python-requests python-setuptools python-six python-support python-talloc python-urllib3 python-wheel python2.7 python2.7-minimal python3-apt python3-chardet python3-colorama python3-debian python3-dev python3-distlib python3-html5lib python3-minimal python3-pil python3-pkg-resources python3-requests python3-setuptools python3-six python3-urllib3 python3-wheel qdbus qjackctl qtchooser qtcore4-l10n rename rpcbind rsync ruby ruby2.1 rubygems-integration samba-common samba-libs scrot sgml-base shared-mime-info squeak-plugins-scratch squeak-vm supercollider supercollider-common supercollider-ide supercollider-language supercollider-server supercollider-supernova tcl8.5 tcpd tk8.5 tk8.6-blt2.5 triggerhappy ucf udisks2 uno-libs3 ure va-driver-all vdpau-va-driver wireless-regdb x11-common x11-utils x11-xkb-utils x11-xserver-utils xauth xdg-user-dirs xfce-keyboard-shortcuts xfconf xfonts-100dpi xfonts-encodings xfonts-utils xkb-data xml-core xserver-common xserver-xorg-core xserver-xorg-input-all xserver-xorg-input-evdev xserver-xorg-input-synaptics zenity-common zlib1g-dev acl adduser alacarte alsa-utils apt apt-utils aptitude aptitude-common avahi-daemon base-files base-passwd bash bash-completion bsdmainutils bsdutils build-essential ca-certificates cifs-utils claws-mail console-setup coreutils cpio crda cron curl dash debconf debconf-i18n debconf-utils debian-reference-en debianutils desktop-base desktop-file-utils dhcpcd5 diffutils dillo dmidecode dmsetup dosfstools dphys-swapfile dpkg e2fslibs e2fsprogs ed epiphany-browser fake-hwclock fbset findutils firmware-atheros firmware-brcm80211 firmware-libertas firmware-ralink firmware-realtek fonts-dejavu fonts-sil-gentium-basic galculator gcc-4.9-base gdb git-core gksu gnome-icon-theme gnome-themes-standard-data gnupg gpgv gpicview  grep groff-base gstreamer1.0-alsa gstreamer1.0-libav gstreamer1.0-plugins-bad gstreamer1.0-plugins-base gstreamer1.0-plugins-good gstreamer1.0-x gtk2-engines gvfs-backends gvfs-fuse gzip hardlink hostname idle idle3 ifupdown info init init-system-helpers initramfs-tools initscripts insserv install-info iproute2 iptables iputils-ping isc-dhcp-client isc-dhcp-common java-common keyboard-configuration klibc-utils kmod leafpad less libacl1 libapt-inst1.5 libapt-pkg4.12 libattr1 libaudit-common libaudit1 libblkid1 libbsd0 libbz2-1.0 libc-bin libc6 libcap2 libcap2-bin libcomerr2 libcryptsetup4 libcwidget3 libdb5.3 libdbus-1-3 libdebconfclient0 libdevmapper1.02.1 libdns-export100 libdrm2 libestr0 libffi6 libfreetype6-dev libgcc1 libgcrypt20 libgdbm3 libgl1-mesa-dri libgles1-mesa libgles2-mesa libgmp10 libgnutls-deb0-28 libgnutls-openssl27 libgpg-error0 libhogweed2 libicu52 libident libidn11 libirs-export91 libisc-export95 libisccfg-export90 libjson-c2 libklibc libkmod2 liblocale-gettext-perl liblogging-stdlog0 liblognorm1 liblzma5 libmount1 libncurses5 libncursesw5 libnettle4 libnewt0.52 libnfnetlink0 libnih-dbus1 libnih1 libp11-kit0 libpam-modules libpam-modules-bin libpam-runtime libpam0g libpcre3 libpipeline1 libpng12-0 libpopt0 libprocps3 libpsl0 libreadline6 libreoffice libreoffice-avmedia-backend-gstreamer libreoffice-base libreoffice-calc libreoffice-draw libreoffice-gtk libreoffice-impress libreoffice-java-common libreoffice-math libreoffice-report-builder-bin libreoffice-sdbc-hsqldb libreoffice-writer libselinux1 libsemanage-common libsemanage1 libsepol1 libservlet2.5-java libsigc++-1.2-5c2 libsigc++-2.0-0c2a libslang2 libsmartcols1 libsqlite3-0 libss2 libssl1.0.0 libstdc++6 libsysfs2 libsystemd0 libtasn1-6 libtext-charwidth-perl libtext-iconv-perl libtext-wrapi18n-perl libtinfo5 libudev1 libusb-0.1-4 libustr-1.0-1 libuuid1 libxapian22 libxtables10 lightdm locales login logrotate lsb-base lua5.1 luajit lxappearance lxappearance-obconf lxde lxde-common lxde-core lxde-icon-theme lxinput lxpanel lxrandr lxtask lxterminal makedev man-db manpages manpages-dev mawk menu-xdg module-init-tools mount mountall multiarch-support nano ncdu ncurses-base ncurses-bin net-tools netbase netcat-openbsd netcat-traditional netsurf-gtk nfs-common ntp openbox  parted passwd pcmanfm perl-base pkg-config plymouth policykit-1 procps psmisc  python-pygame python-serial python-tk python3  python3-numpy python3-pip python3-serial python3-tk python3-uno readline-common rsyslog scratch sed sensible-utils ssh startpar strace sudo systemd systemd-sysv sysv-rc sysvinit-utils tar tasksel tasksel-data timidity traceroute tree tzdata udev udisks unzip usbutils util-linux v4l-utils vim-common vim-tiny wget whiptail wireless-tools wpasupplicant x2x xarchiver xcompmgr xdg-utils xinit xpdf xserver-xorg xserver-xorg-video-fbdev xz-utils zenity zlib1g
```

# Lenovo IdeaPad A10 specifications

* 10.1-inch (1366 x 768 pixels) 10-point multi-touch display
* 1.6GHz quad-core ARM Cortex A9 processor
* Lenovo customized Android 4.2 OS
* Dimensions: 269 mm x 185 mm x 17.3 mm; Weight: 1 kg (approx.)
* 0.3MP front-facing camera
* 1 GB DDR3 RAM, 16 GB internal memory
* 1 Micro USB, 2 USB 2.0, Micro HDMI, TF, (Micro SD) card reader, Audio Combo Jack, (headphone and mic)
* Integrated speakers
* AccuType keyboard
* 2 cell 22.6WH battery that offers upto 9 hours video playback and up to 39 hours audio playback
