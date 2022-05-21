pkgname=holoiso-main
pkgver="snapshot$(date +%Y%m%d.%H%M)"
pkgdesc="HoloISO base installation"
pkgrel="1"
depends=('archlinux-keyring' 'ark' 'cheese' 'chromium' 'cups' 'curl' 'dolphin' 'ffmpegthumbs' 'gamescope' 'git' 'glxinfo' 'go' 'gwenview' 'hunspell' 'hunspell-en_us' 'jupiter-hw-support' 'kdegraphics-thumbnailers' 'konsole' 'kwrite' 'lib32-pipewire' 'lib32-pipewire-jack' 'lib32-pipewire-v4l2' 'lib32-vulkan-radeon' 'mangohud' 'holoiso-updateclient' 'noto-fonts-cjk' 'pipewire' 'pipewire-alsa' 'pipewire-jack' 'wireplumber' 'pipewire-pulse' 'pipewire-v4l2' 'plasma-meta' 'plasma-nm' 'print-manager' 'spectacle' 'steam-jupiter-stable' 'steamdeck-kde-presets' 'tar' 'ufw' 'vlc' 'vulkan-radeon' 'yay' 'wget' 'zsh')
arch=("x86_64")

package() {
    holoiso_basever="SteamOS_Holo-$(date +%Y%m%d_%H%M)_amdgpu-x86_64"
    holoiso_codename="Lord Gaben's treasure (snapshot2)"
    mkdir -p "${pkgdir}/usr/bin"
    mkdir -p "${pkgdir}/etc"
    mkdir -p "${pkgdir}/etc/udev"    
    mkdir -p "${pkgdir}/etc/udev/rules.d"    
    cp "${srcdir}/99-oxpgamepad.rules" "${pkgdir}/etc/udev/rules.d/99-oxpgamepad.rules"    
    cp "${srcdir}/steamos-session-select" "${pkgdir}/usr/bin/steamos-session-select"
    cp "${srcdir}/gamescope-session" "${pkgdir}/usr/bin/gamescope-session"
    cp "${srcdir}/jupiter-controller-update" "${pkgdir}/usr/bin/jupiter-controller-update"        
    cp "${srcdir}/osinfo" "${srcdir}/osinfo_tmp"
    sed -i "s/snapshotver/snapshot$(date +%Y%m%d.%H%M)/g" osinfo_tmp
    sed -i "s/versionver/${holoiso_codename}/g" osinfo_tmp
    sed -i "s/buildver/${holoiso_basever}/g" osinfo_tmp
    cp "${srcdir}/osinfo_tmp" "${pkgdir}/etc/os-release"
    rm "${srcdir}/osinfo_tmp"
    chmod +x "${pkgdir}/usr/bin/steamos-session-select"
    chmod +x "${pkgdir}/usr/bin/gamescope-session"    
}

