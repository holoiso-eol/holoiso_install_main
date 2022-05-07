pkgname=holoiso-main
pkgver="snapshot$(date +%Y%m%d.%H%M)"
pkgdesc="HoloISO base installation"
pkgrel="1"
depends=('archlinux-keyring' 'cheese' 'chromium' 'cups' 'curl' 'dolphin' 'ffmpegthumbs' 'gamescope' 'git' 'glxinfo' 'go' 'gwenview' 'hunspell' 'hunspell-en_us' 'jupiter-hw-support' 'kdegraphics-thumbnailers' 'konsole' 'kwrite' 'lib32-pipewire' 'lib32-pipewire-jack' 'lib32-pipewire-v4l2' 'lib32-vulkan-radeon' 'mangohud' 'noto-fonts-cjk' 'pipewire' 'pipewire-alsa' 'pipewire-jack' 'pipewire-media-session' 'pipewire-pulse' 'pipewire-v4l2' 'plasma-meta' 'plasma-nm' 'print-manager' 'spectacle' 'steam-jupiter-stable' 'steamdeck-kde-presets' 'tar' 'ufw' 'vlc' 'vulkan-radeon' 'yay' 'wget' 'zsh')
arch=("x86_64")

package() {
    holoiso_basever="SteamOS_Holo-$(date +%Y%m%d_%H%M)_amdgpu-x86_64"
    holoiso_codename="Boop (snapshot1)"
    mkdir -p "${pkgdir}/usr/bin"
    mkdir -p "${pkgdir}/etc"
    cp "${srcdir}/steamos-update" "${pkgdir}/usr/bin/steamos-update"
    cp "${srcdir}/steamos-session-select" "${pkgdir}/usr/bin/steamos-session-select"
    cp "${srcdir}/osinfo" "${srcdir}/osinfo_tmp"
    sed -i "s/snapshotver/snapshot$(date +%Y%m%d.%H%M)/g" osinfo_tmp
    sed -i "s/versionver/${holoiso_codename}/g" osinfo_tmp
    sed -i "s/buildver/${holoiso_basever}/g" osinfo_tmp
    cp "${srcdir}/osinfo_tmp" "${pkgdir}/etc/os-release"
    chmod +x "${pkgdir}/usr/bin/steamos-session-select"
    chmod +x "${pkgdir}/usr/bin/steamos-update"
}

