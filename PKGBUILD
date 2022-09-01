# Maintainer: Antonio Rojas <arojas@archlinux.org>
# Maintainer: Felix Yan <felixonmars@archlinux.org>
# Contributor: Andrea Scarpino <andrea@archlinux.org>
# Contributor: Douglas Soares de Andrade <douglas@archlinux.org>
# Contributor: riai <riai@bigfoot.com>, Ben <ben@benmazer.net>

pkgbase=sip4
pkgname=(sip4 python-sip4)
pkgver=4.19.25
pkgrel=3
arch=(x86_64)
url='https://www.riverbankcomputing.com/software/sip/intro'
license=('custom:"sip"')
makedepends=(python)
source=("https://www.riverbankcomputing.com/static/Downloads/sip/$pkgver/sip-$pkgver.tar.gz")
sha256sums=('b39d93e937647807bac23579edbff25fe46d16213f708370072574ab1f1b4211')

prepare() {
  mkdir -p build
}

build() {
  cd build
  python ../sip-$pkgver/configure.py CFLAGS="$CFLAGS" LFLAGS="$LDFLAGS"
  make
}

package_sip4() {
  pkgdesc="A tool that makes it easy to create Python bindings for C and C++ libraries"
  depends=(glibc)
  replaces=('sip<5')

  cd build
  make DESTDIR="$pkgdir" install -C sipgen
# move sip.h to /usr/include
  mv "$pkgdir"/usr/include/{python*/sip.h,}
  rm -r "$pkgdir"/usr/include/python*

  install -Dm644 ../sip-$pkgver/LICENSE "$pkgdir"/usr/share/licenses/$pkgname/LICENSE
}

package_python-sip4() {
  pkgdesc="Python SIP4 bindings for C and C++ libraries"
  depends=(python)
  provides=(python-sip)
  replaces=(python-sip)

  cd build
  make DESTDIR="$pkgdir" install
  rm -r "$pkgdir"/usr/{bin,include} # conflicts with sip

  install -Dm644 ../sip-$pkgver/LICENSE "$pkgdir"/usr/share/licenses/$pkgname/LICENSE
}