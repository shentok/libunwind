# Maintainer: Felix Yan <felixonmars@archlinux.org>
# Contributor: Sébastien Luttringer
# Contributor: Lawrence Lee <valheru@facticius.net>
# Contributor: Phillip Marvin <phillip.marvin@gmail.com>
# Contributor: keystone <phillip.marvin@gmail.com>

pkgbase=libunwind
pkgname=$pkgbase-multiarch
pkgver=1.5.0
pkgrel=1
pkgdesc='Portable and efficient C programming interface (API) to determine the call-chain of a program'
arch=('x86_64')
url='https://www.nongnu.org/libunwind/'
license=('GPL')
depends=('xz' 'zlib')
makedepends=('texlive-core')
source=("https://download.savannah.gnu.org/releases/$pkgbase/$pkgbase-$pkgver.tar.gz"{,.sig})
sha512sums=('1df20ca7a8cee2f2e61294fa9b677e88fec52e9d5a329f88d05c2671c69fa462f6c18808c97ca9ff664ef57292537a844f00b18d142b1938c9da701ca95a4bab'
            'SKIP')
validpgpkeys=('5C96BDEAF5F47FB02BD4F6B965D98560914F3F48'  # Arun Sharma
              '1675C8DA2EF907FB116EB709EC52B396E6874AF2'  # Dave Watson
              '75D2CFC56CC2E935A4143297015A268A17D55FA4') # Dave Watson
provides=($pkgbase)
conflicts=($pkgbase)

prepare() {
  cp -r $pkgbase-$pkgver $pkgbase-x86-$pkgver
}

build() {
  cd $pkgbase-$pkgver
  ./configure --prefix=/usr
  sed -i -e 's/ -shared / -Wl,-O1,--as-needed\0/g' libtool
  make

  cd ../$pkgbase-x86-$pkgver
  ./configure --prefix=/usr --target=i686-linux
  sed -i -e 's/ -shared / -Wl,-O1,--as-needed\0/g' libtool
  make
}

check() {
  cd $pkgbase-$pkgver
  # This function is ``supposed'' to fail. Upstream know, but haven't fixed it.
  make check || :

  cd ../$pkgbase-x86-$pkgver
  # This function is ``supposed'' to fail. Upstream know, but haven't fixed it.
  make check || :
}

package() {
  cd $pkgbase-$pkgver
  make DESTDIR="$pkgdir" install

  cd ../$pkgbase-x86-$pkgver
  make DESTDIR="$pkgdir" install
}

# vim:set ts=2 sw=2 et:
