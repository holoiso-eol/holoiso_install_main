pkgname=holoiso-main
pkgver="snapshot$(date +%Y%m%d.%H%M)"
pkgdesc="HoloISO OS Image version 4 (snapshot$(date +%Y%m%d.%H%M))"
pkgrel="1"
install=holo.install
depends=('archlinux-keyring' 'steamos-systemreport' 'handygccs-git' 'ark' 'cheese' 'cups' 'curl' 'dolphin' 'ffmpegthumbs' 'gamescope-holoiso' 'git' 'glxinfo' 'go' 'gwenview' 'hunspell' 'hunspell-en_us' 'holo-wireplumber' 'kdegraphics-thumbnailers' 'konsole' 'kwrite' 'lib32-pipewire' 'lib32-pipewire-jack' 'lib32-pipewire-v4l2' 'libva' 'lib32-libva' 'libva-utils' 'libva-mesa-driver' 'libva-intel-driver' 'lib32-libva-mesa-driver' 'lib32-libva-intel-driver' 'lib32-vulkan-radeon' 'lib32-vulkan-intel' 'mangohud' 'mesa' 'lib32-mesa' 'holoiso-updateclient' 'noto-fonts-cjk' 'pipewire' 'pipewire-alsa' 'pipewire-jack' 'wireplumber' 'pipewire-pulse' 'pipewire-v4l2' 'plasma-meta' 'plasma-nm' 'print-manager' 'spectacle' 'steam-jupiter-stable' 'tar' 'ufw' 'vlc' 'vulkan-intel' 'vulkan-radeon' 'wget' 'zsh' 'xbindkeys' 'steam-im-modules' 'systemd-swap' 'ttf-twemoji-default' 'ttf-hack' 'ttf-dejavu' 'pkgconf' 'pavucontrol' 'partitionmanager' 'gamemode' 'lib32-gamemode' 'bluez-plugins' 'bluez-utils' 'xf86-video-amdgpu' 'xf86-video-intel' 'python-evdev'
         'dmidecode' # for jupiter-biosupdate
         'python-crcmod' 'python-click' 'python-progressbar' 'python-hid'
         'jq' # for jupiter-controller-update, jupiter-biosupdate
         'alsa-utils' # for the sound workarounds
         'parted' 'e2fsprogs' # for sdcard formatting
         'udisks2>=2.9.4-1.1' # for mounting external drives with the 'as-user' option
        'kdialog')
makedepends=('rsync' 'git' 'openssh' 'xorg-xcursorgen')
arch=("x86_64")

package() {
    holoiso_codename="Image ($(echo $RANDOM | md5sum | head -c 10; echo;))"
    ## steamos-customizations and jupiter-legacy-support
    cp -r "${srcdir}/new_steamos_dirs/etc" "${pkgdir}"
    cp -r "${srcdir}/new_steamos_dirs/usr" "${pkgdir}"
    cp -r "${srcdir}/steamos-customizations/etc" "${pkgdir}"
    cp -r "${srcdir}/steamos-customizations/usr" "${pkgdir}"
    ##


    ## Create and properly chmod directories
    chmod -R 644 "${pkgdir}/etc"
    chmod -R 644 "${pkgdir}/usr"
    chmod -R +x "${pkgdir}/usr/bin"
    chmod -R 644 "${pkgdir}/etc/flatpak"
    chmod -R 755 "${pkgdir}/usr/lib"
    chmod -R 755 "${pkgdir}/etc/systemd"
    chmod -R +x "${pkgdir}/usr/share"
    mkdir -p "${pkgdir}/usr/bin"
    mkdir -p "${pkgdir}/etc"
    mkdir -p "${pkgdir}/etc/systemd/logind.conf.d"
    mkdir -p "${pkgdir}/etc/udev"    
    mkdir -p "${pkgdir}/etc/udev/rules.d"    
    mkdir -p "${pkgdir}/usr/lib/systemd/system"
    mkdir -p "${pkgdir}/etc/skel/Desktop" 
    mkdir -p "${pkgdir}/etc/xdg/autostart"
    mkdir -p "${pkgdir}/usr/bin/steamos-polkit-helpers"
    mkdir -p "${pkgdir}/etc/pacman.d"
    ##

    ## HoloISO snapshot info and configurations
    cp "${srcdir}/holomirror" "${pkgdir}/etc/pacman.d/holo_mirrorlist"
    cp "${srcdir}/osinfo" "${srcdir}/osinfo_tmp"
    cp "${srcdir}/pacman.conf" "${pkgdir}/etc/pacman.conf"
    cp "${srcdir}/stable_pacman.conf" "${pkgdir}/etc/stable_pacman.conf"
    sed -i "s/snapshotver/snapshot$(date +%Y%m%d.%H%M)/g" osinfo_tmp
    sed -i "s/versionver/4/g" osinfo_tmp
    sed -i "s/buildver/${holoiso_codename}/g" osinfo_tmp
    cp "${srcdir}/osinfo_tmp" "${pkgdir}/etc/os-release"
    rm "${srcdir}/osinfo_tmp"
    cp "${srcdir}/holoiso-branch" "${pkgdir}/etc/holoiso-branch"
    ##
   
    cp "${srcdir}/steamos-session-select" "${pkgdir}/usr/bin/steamos-session-select"
    cp "${srcdir}/steamos-select-branch" "${pkgdir}/usr/bin/steamos-select-branch"
    cp "${srcdir}/holoiso-disable-sessions" "${pkgdir}/usr/bin/holoiso-disable-sessions"  
    cp "${srcdir}/holoiso-enable-sessions" "${pkgdir}/usr/bin/holoiso-enable-sessions"          
    cp "${srcdir}/steamos-gamemode.desktop" "${pkgdir}/etc/skel/Desktop/steamos-gamemode.desktop"
    cp "${srcdir}/holoiso-grub-update" "${pkgdir}/usr/bin/holoiso-grub-update"
    cp -r "${srcdir}/logind.conf.d/" "${pkgdir}/etc/systemd/"
    cp "${srcdir}/99-dualshock-dualsense.rules" "${pkgdir}/etc/udev/rules.d/99-dualshock-dualsense.rules"
    chmod +x "${pkgdir}/usr/bin/steamos-session-select"  
    chmod +x "${pkgdir}/usr/bin/holoiso-disable-sessions"
    chmod +x "${pkgdir}/usr/bin/steamos-select-branch"
    chmod +x "${pkgdir}/usr/bin/holoiso-enable-sessions"
    chmod +x "${pkgdir}/etc/skel/Desktop/steamos-gamemode.desktop"
    chmod +x "${pkgdir}/usr/bin/holoiso-grub-update"
    echo "Release output:"
    cat "${pkgdir}/etc/os-release"

    ## jupiter-hw-support
    git clone https://gitlab.com/evlaV/jupiter-hw-support/ ${srcdir}/jupiter-hw-support
    rsync -a "$srcdir"/jupiter-hw-support/* "$pkgdir"
    cd $pkgdir/usr/share/steamos/
    xcursorgen $pkgdir/usr/share/steamos/steamos-cursor-config $pkgdir/usr/share/icons/steam/cursors/default
    cd "$pkgdir/usr/share/jupiter_bios_updater"
      # Remove gtk2 binary and respective build/start script - unused
      # Attempts to use gtk2 libraries which are not on the device.
    rm h2offt-g H2OFFTx64-G.sh
      # Driver module -- doesn't currently build, and not supported
    rm -rf driver
    cd $pkgdir/..
    cp -f "${srcdir}/jupiter-controller-update" "${pkgdir}/usr/bin/jupiter-controller-update"
    cp -f "${srcdir}/jupiter-biosupdate" "${pkgdir}/usr/bin/jupiter-biosupdate"
    cp -f "${srcdir}/steamos-priv-write" "${pkgdir}/usr/bin/steamos-polkit-helpers/steamos-priv-write"
    chmod +x "${pkgdir}/usr/bin/jupiter-controller-update" 
    chmod +x "${pkgdir}/usr/bin/jupiter-biosupdate" 
    chmod +x "${pkgdir}/usr/bin/steamos-polkit-helpers/steamos-priv-write"
    rm -rf "${pkgdir}/usr/lib/udev/rules.d/99-steamos-automount.rules"
    ##

    ## steamdeck-kde-presets
    git clone https://gitlab.com/evlaV/steamdeck-kde-presets ${srcdir}/steamdeck-kde-presets
    cp -R "$srcdir"/steamdeck-kde-presets/* "$pkgdir"
        ## Nuke stuff that we don't REALLY need from Deck at all
        rm -rf "${pkgdir}/etc/X11/Xsession.d/50rotate-screen"
        rm -rf "${pkgdir}/etc/sddm.conf.d/"
        rm -rf "${pkgdir}/usr/bin/jupiter-plasma-bootstrap"
    cp "$srcdir"/50rotate-screen "${pkgdir}/etc/X11/Xsession.d/50rotate-screen"
    chmod +x "${pkgdir}/etc/X11/Xsession.d/50rotate-screen"
    chmod 0644 "${pkgdir}/usr/share/polkit-1/actions/org.jittleyang.deeznuts.policy"
    ##

    ## Device shit
    cp "$srcdir"/holoiso-devicequirk-set "${pkgdir}/usr/bin/holoiso-devicequirk-set"
    cp "$srcdir"/holoiso-devicequirk-generator "${pkgdir}/usr/bin/genquirks"
    chmod +x "${pkgdir}/usr/bin/holoiso-devicequirk-set"
    chmod +x "${pkgdir}/usr/bin/genquirks"
    git clone https://github.com/HoloISO/him_devicequirks "${pkgdir}/usr/lib/holoiso-hwsupport/him_devicequirks"
    echo "Cleaning up..."
    rm -rf ${srcdir}/jupiter-hw-support
    rm -rf ${srcdir}/steamdeck-kde-presets
}

