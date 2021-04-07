pkgname=bsrv
pkgver=0.0.1
pkgrel=1
pkgdesc='daemon to schedule and run borg backups automatically'
url='https://github.com/alx-g/bsrv'
license=('custom:BSD 3-clause')
arch=('any')
depends=('python'
         'gobject-introspection'
         'qt5-base'
         'libsystemd')
makedepends=('python-setuptools'
             'python-pip')
checkdepends=()
backup=()
source=("$pkgname-$pkgver.tar.gz::https://files.alx-g.de/$pkgname/$pkgname-$pkgver.tar.gz")
sha256sums=('c09bfc3be4f104c8a8b8f79df803b52551108c821af54450e1805ffa7e4c0d14')
install='bsrv.install'

prepare() {
    # Setup all absolute paths in shell scripts
    cd "$srcdir/"
    sed -i "s|{{INSTALL_DIR}}|/usr/lib/$pkgname|g" ./src/bsrvd.sh
    sed -i "s|{{INSTALL_DIR}}|/usr/lib/$pkgname|g" ./src/bsrvstatd.sh
    sed -i "s|{{INSTALL_DIR}}|/usr/lib/$pkgname|g" ./src/bsrvcli.sh
    sed -i "s|{{INSTALL_DIR}}|/usr/lib/$pkgname|g" ./src/bsrvtray.sh
    sed -i "s|{{PKGDIR}}||g" "./configs/systemd/bsrvd.service"
    sed -i "s|{{PKGDIR}}||g" "./configs/systemd/bsrvstatd.service"
}

package() {
    # Install dbus and systemd config files
    cd "$srcdir/"
    install -Dm644 configs/dbus/de.alxg.bsrvd.conf "$pkgdir"/usr/share/dbus-1/system.d/de.alxg.bsrvd.conf
    install -Dm644 configs/dbus/de.alxg.bsrvd.service "$pkgdir"/usr/share/dbus-1/system-services/de.alxg.bsrvd.service
    install -Dm644 configs/systemd/bsrvd.service "$pkgdir"/usr/lib/systemd/system/bsrvd.service
    install -Dm644 configs/systemd/bsrvstatd.service "$pkgdir"/usr/lib/systemd/system/bsrvstatd.service

    # Install BSD 3-clause LICENSE
    install -Dm644 LICENSE "$pkgdir"/usr/share/licenses/$pkgname/LICENSE

    # Install bsrv software files
    cd "src"
    mkdir -p "$pkgdir/usr/lib/$pkgname"
    cp "bsrv" "$pkgdir/usr/lib/$pkgname/" -r
    cp "bsrvd" "$pkgdir/usr/lib/$pkgname/" -r
    cp "bsrvstatd" "$pkgdir/usr/lib/$pkgname/" -r
    cp "bsrvcli" "$pkgdir/usr/lib/$pkgname/" -r
    cp "bsrvtray" "$pkgdir/usr/lib/$pkgname/" -r
    cp "bsrvd.sh" "$pkgdir/usr/lib/$pkgname/"
    cp "bsrvstatd.sh" "$pkgdir/usr/lib/$pkgname/"
    cp "bsrvcli.sh" "$pkgdir/usr/lib/$pkgname/"
    cp "bsrvtray.sh" "$pkgdir/usr/lib/$pkgname/"
    cp "requirements.txt" "$pkgdir/usr/lib/$pkgname/"
    chmod 644 "$pkgdir/usr/lib/$pkgname" -R
    chmod +X  "$pkgdir/usr/lib/$pkgname" -R
    chmod 755 "$pkgdir/usr/lib/$pkgname/bsrvd.sh"
    chmod 755 "$pkgdir/usr/lib/$pkgname/bsrvstatd.sh"
    chmod 755 "$pkgdir/usr/lib/$pkgname/bsrvcli.sh"
    chmod 755 "$pkgdir/usr/lib/$pkgname/bsrvtray.sh"

    # Install bsrv assets
    cd ../
    mkdir -p "$pkgdir/usr/share/$pkgname"
    cp "assets" "$pkgdir/usr/share/$pkgname/" -r
    chmod 644 "$pkgdir/usr/share/$pkgname" -R
    chmod +X  "$pkgdir/usr/share/$pkgname" -R
}
