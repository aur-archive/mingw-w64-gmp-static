pkgname=mingw-w64-gmp-static
pkgver=5.1.1
pkgrel=1
pkgdesc="A free library for arbitrary precision arithmetic (mingw-w64, static)"
arch=(any)
url="http://gmplib.org"
license=("LGPL3")
makedepends=(mingw-w64-gcc)
depends=(mingw-w64-crt)
conflicts=(mingw-w64-gmp)
provides=(mingw-w64-gmp)
options=(!libtool !strip !buildflags)
source=("ftp://ftp.gmplib.org/pub/gmp-${pkgver}/gmp-${pkgver}.tar.xz")
md5sums=('485b1296e6287fa381e6015b19767989')

_architectures="i686-w64-mingw32 x86_64-w64-mingw32"

build() {
  unset LDFLAGS
  for _arch in ${_architectures}; do
    mkdir -p "${srcdir}/${pkgname}-${pkgver}-build-${_arch}"
    cd "${srcdir}/${pkgname}-${pkgver}-build-${_arch}"
    ${srcdir}/gmp-${pkgver}/configure \
      --prefix=/usr/${_arch} \
      --build=$CHOST \
      --host=${_arch} \
      --enable-cxx
    make
  done
}

package() {
  for _arch in ${_architectures}; do
    cd "${srcdir}/${pkgname}-${pkgver}-build-${_arch}"
    make DESTDIR="$pkgdir" install
    find "$pkgdir/usr/${_arch}" -name '*.a' | xargs -rtl1 ${_arch}-strip -g
    rm -r "$pkgdir/usr/${_arch}/share"
  done
}
