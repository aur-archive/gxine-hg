# See AUR interface to contact current maintainer.

pkgname=gxine-hg
pkgver=r2285.e05f58d2b749
pkgrel=3
pkgdesc="GTK+ frontend for xine. Development version."
arch=('i686' 'x86_64')
url="http://www.xine-project.org/"
license=('GPL')
conflicts=('gxine')
provides=('gxine')
depends=('xine-lib' 'gtk2' 'js185' 'dbus-glib' 'lirc'
	 'desktop-file-utils' 'hicolor-icon-theme')
makedepends=('libxaw' 'autoconf' 'mercurial')
optdepends=('libxaw: Mozilla browser plugin')
options=('!libtool')
install="$pkgname.install"
source=("$pkgname::hg+http://anonscm.debian.org/hg/xine-lib/gxine/")
md5sums=('SKIP')

pkgver() {
  cd "$srcdir/$pkgname"
  #
  # In mercurial, you cannot assure that id -n is equal in two copies
  # of the same repository!!!!! If the repo is changed somehere else,
  # it will be a mess. So let's try this and hope for the best.
  # 
  printf "r%s.%s" "$(hg identify -n)" "$(hg identify -i)"
}

build() {
  cd "$srcdir/$pkgname"

  ./autogen.sh

  ./configure --prefix=/usr \
              --sysconfdir=/etc \
              --disable-integration-wizard \
              --without-browser-plugin \
              --with-logo-format=image \
              --with-dbus \
              --with-gudev \
              --with-pic \
              --enable-watchdog \
	      --disable-rpath \
              --disable-deprecated \
              --disable-own-playlist-parsers \
              VENDOR_PKG_VERSION="$pkgver-$pkgrel; Arch Linux"

  make
}

package() {
  cd "$srcdir/$pkgname"

  make DESTDIR="$pkgdir/" install

  # mozilla plugin
  install -d "$pkgdir/usr/lib/mozilla/plugins"
  ln -s /usr/lib/gxine/gxineplugin.so \
    "$pkgdir/usr/lib/mozilla/plugins"
}
