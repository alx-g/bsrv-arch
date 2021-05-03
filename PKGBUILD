pkgbase=bsrv
pkgname=($pkgbase
         $pkgbase-tray)
pkgver=0.0.2
pkgrel=1
pkgdesc='daemon to schedule and run borg backups automatically'
url='https://github.com/alx-g/bsrv'
license=('custom:BSD 3-clause')
arch=('any')
depends=('python'
         'python-cairo'
         'python-gobject'
         'gobject-introspection'
         'borg'
         'libsystemd')
makedepends=('python-setuptools'
             'python-pip')
checkdepends=()
backup=()
source=("$pkgbase-$pkgver.tar.gz::https://github.com/alx-g/$pkgbase/archive/refs/tags/v$pkgver.tar.gz")
sha256sums=('bd36643cd32a68af32edc2ae6047cc569016a12c7dcf8291e7aab32c616c5e66')
install='bsrv.install'

prepare() {
    # Setup all absolute paths in shell scripts
    cd "$srcdir/$pkgbase-$pkgver"
    sed -i "s|{{INSTALL_DIR}}|/usr/lib/$pkgbase|g" ./src/bsrvd.sh
    sed -i "s|{{INSTALL_DIR}}|/usr/lib/$pkgbase|g" ./src/bsrvstatd.sh
    sed -i "s|{{INSTALL_DIR}}|/usr/lib/$pkgbase|g" ./src/bsrvcli.sh
    sed -i "s|{{INSTALL_DIR}}|/usr/lib/$pkgbase|g" ./src/bsrvtray.sh
    sed -i "s|{{PKGDIR}}||g" "./configs/systemd/bsrvd.service"
    sed -i "s|{{PKGDIR}}||g" "./configs/systemd/bsrvstatd.service"
}

package_bsrv() {
    # Install dbus and systemd config files
    cd "$srcdir/$pkgbase-$pkgver"
    install -Dm644 configs/dbus/de.alxg.bsrvd.conf "$pkgdir"/usr/share/dbus-1/system.d/de.alxg.bsrvd.conf
    install -Dm644 configs/dbus/de.alxg.bsrvd.service "$pkgdir"/usr/share/dbus-1/system-services/de.alxg.bsrvd.service
    install -Dm644 configs/systemd/bsrvd.service "$pkgdir"/usr/lib/systemd/system/bsrvd.service
    install -Dm644 configs/systemd/bsrvstatd.service "$pkgdir"/usr/lib/systemd/system/bsrvstatd.service

    # Install BSD 3-clause LICENSE
    install -Dm644 LICENSE "$pkgdir"/usr/share/licenses/$pkgbase/LICENSE

    # Install bsrv software files
    cd "src"
    mkdir -p "$pkgdir/usr/lib/$pkgbase"
    cp "bsrv" "$pkgdir/usr/lib/$pkgbase/" -r
    cp "bsrvd" "$pkgdir/usr/lib/$pkgbase/" -r
    cp "bsrvstatd" "$pkgdir/usr/lib/$pkgbase/" -r
    cp "bsrvcli" "$pkgdir/usr/lib/$pkgbase/" -r
    cp "bsrvd.sh" "$pkgdir/usr/lib/$pkgbase/"
    cp "bsrvstatd.sh" "$pkgdir/usr/lib/$pkgbase/"
    cp "bsrvcli.sh" "$pkgdir/usr/lib/$pkgbase/"
    cp "requirements.txt" "$pkgdir/usr/lib/$pkgbase/"
    chmod 644 "$pkgdir/usr/lib/$pkgbase" -R
    chmod +X  "$pkgdir/usr/lib/$pkgbase" -R
    chmod 755 "$pkgdir/usr/lib/$pkgbase/bsrvd.sh"
    chmod 755 "$pkgdir/usr/lib/$pkgbase/bsrvstatd.sh"
    chmod 755 "$pkgdir/usr/lib/$pkgbase/bsrvcli.sh"

    # make venv dir so pacman knows about it
    mkdir "$pkgdir/usr/lib/$pkgbase/venv"

    # Touch /usr/bin symlinks so pacman knows about them
    mkdir "$pkgdir/usr/bin"
    touch "$pkgdir/usr/bin/bsrvd"
    touch "$pkgdir/usr/bin/bsrvstatd"
    touch "$pkgdir/usr/bin/bsrvcli"
}

package_bsrv-tray() {
    depends=(
         'qt5-base'
         'bsrv')
    install='bsrv-tray.install'
    pkgdesc='status tray icon for bsrv daemon'

    cd "$srcdir/$pkgbase-$pkgver"

    cd "src"
    # Install bsrv software files
    mkdir -p "$pkgdir/usr/lib/$pkgbase"
    cp "bsrvtray" "$pkgdir/usr/lib/$pkgbase/" -r
    cp "bsrvtray.sh" "$pkgdir/usr/lib/$pkgbase/"
    cp "requirements_tray.txt" "$pkgdir/usr/lib/$pkgbase/"
    chmod 644 "$pkgdir/usr/lib/$pkgbase" -R
    chmod +X  "$pkgdir/usr/lib/$pkgbase" -R
    chmod 755 "$pkgdir/usr/lib/$pkgbase/bsrvtray.sh"

    # Install bsrv assets
    cd ../
    mkdir -p "$pkgdir/usr/share/$pkgbase"
    cp "assets" "$pkgdir/usr/share/$pkgbase/" -r
    chmod 644 "$pkgdir/usr/share/$pkgbase" -R
    chmod +X  "$pkgdir/usr/share/$pkgbase" -R

    # Touch /usr/bin symlinks so pacman knows about them
    mkdir "$pkgdir/usr/bin"
    touch "$pkgdir/usr/bin/bsrvtray"
}
