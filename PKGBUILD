# Maintainer: Alesh Slovak <aleshslovak@gmail.com>

pkgname=chimera
pkgver='0.14.8'
pkgrel='1'
pkgdesc="Configure and manage games in Steam"
arch=('any')
url="https://github.com/MrCraigen/chimera"
license=('MIT')
provides=('steam-tweaks' 'steam-buddy')
conflicts=('steam-tweaks' 'steam-buddy')
depends=('python' 'python-bottle' 'python-pyftpdlib' 'python-yaml' 'python-vdf' 'python-inotify-simple' 'python-requests' 'python-beaker' 'python-pygame' 'python-bcrypt' 'python-psutil' 'python-pyudev' 'python-leveldb' 'flatpak' 'xdotool' 'xorg-xprop' 'xorg-xwininfo' 'ponymix' 'legendary' 'ttf-dejavu' 'wyvern' 'innoextract' 'mesa-utils')
optdepends=('srt-live-server' 'steam-removable-media-git') # compiling cores takes a long time, so make them optional
source=("${pkgname}::git+https://github.com/MrCraigen/chimera#branch=master")
md5sums=('SKIP')

pkgver() {
        cd "${srcdir}/${pkgname}"
        git describe --long --tags | sed 's/\([^-]*-g\)/r\1/;s/-/./g'
}

build() {
        cd "${srcdir}/${pkgname}"
        python setup.py build
}
package() {
        cd "${srcdir}/${pkgname}"
        python setup.py install --root="$pkgdir" --prefix=/usr --skip-build
        mkdir -p "$pkgdir/etc/systemd/system"
        mkdir -p "$pkgdir/usr/lib/systemd/user"
        install -m 644 "chimera.service" "$pkgdir/usr/lib/systemd/user/chimera.service"
        install -m 644 "steam-patch.service" "$pkgdir/usr/lib/systemd/user/steam-patch.service"
        install -m 644 "chimera-proxy.service" "$pkgdir/etc/systemd/system/chimera-proxy.service"
        install -m 644 "chimera-proxy.socket" "$pkgdir/etc/systemd/system/chimera-proxy.socket"
}
