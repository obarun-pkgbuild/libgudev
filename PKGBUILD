# Maintainer: Eric Vidal <eric@obarun.org>
# based on the	original https://projects.archlinux.org/svntogit/packages.git/tree/trunk?h=packages/libgudev
# 						Maintainer: Evangelos Foutras <evangelos@foutrelis.com>

pkgname=libgudev
pkgver=232
pkgrel=2
pkgdesc="GObject bindings for libudev"
arch=('x86_64')
url="https://wiki.gnome.org/Projects/libgudev"
license=('LGPL2.1')
depends=('glib2')
makedepends=('gobject-introspection' 'gtk-doc' 'git' 'gnome-common')
provides=('libgudev-1.0.so')
_commit=58eb745d8c4fb06b35706c2c997313235dccb1fc # tags/232^0
source=("git+https://git.gnome.org/browse/libgudev#commit=$_commit")
sha256sums=('SKIP')
validpgpkeys=('6DD4217456569BA711566AC7F06E8FDE7B45DAAC') # Eric Vidal

pkgver() {
  cd $pkgname
  git describe --tags | sed 's/-/+/g'
}

prepare() {
  cd $pkgname
  NOCONFIGURE=1 ./autogen.sh
}

check() {
  cd $pkgname
  make check
}

build() {
  cd "${pkgname}"

  ./configure \
    --prefix=/usr \
    --enable-gtk-doc \
    --disable-umockdev
    sed -i 's/ -shared / -Wl,-O1,--as-needed\0/g' -i libtool
  make
}

package() {
  cd "${pkgname}"
  make DESTDIR="$pkgdir" install
}

# vim:set ts=2 sw=2 et:
