# bsrv-arch
This Repository contains the PKGBUILD for [bsrv](https://github.com/alx-g/bsrv) installation on archlinux.

# Installation

Clone this repository, then run

```bash
makepkg -si
```

in this folder to download and install the latest version of [bsrv](https://github.com/alx-g/bsrv).
This includes `bsrv` and `bsrv-tray`. If you only want to install `bsrv` and exclude the heavy pyqt5 dependency of `bsrv-tray`, you can use

```bash
makepkg -s
pacman -U bsrv-{version}-1-any.pkg.tar.zst
```
