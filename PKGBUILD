# Maintainer: pingplug < aur at pingplug dot me >
# Contributor: Schala Zeal < schalaalexiazeal at gmail dot com >

_architectures="i686-w64-mingw32 x86_64-w64-mingw32"

pkgname=mingw-w64-libunistring
pkgver=1.0
pkgrel=1
pkgdesc="Library for manipulating Unicode strings and C strings (mingw-w64)"
arch=('any')
url="https://www.gnu.org/software/libunistring/"
license=('GPL')
depends=('mingw-w64-crt'
         'mingw-w64-libiconv')
makedepends=('mingw-w64-configure')
options=('!strip' 'staticlibs' '!buildflags')
source=("https://ftp.gnu.org/gnu/libunistring/libunistring-${pkgver}.tar.xz"{,.sig})
sha256sums=('5bab55b49f75d77ed26b257997e919b693f29fd4a1bc22e0e6e024c246c72741'
            'SKIP')
validpgpkeys=('9001B85AF9E1B83DF1BDA942F5BE8B267C6A406D') # Bruno Haible (Open Source Development) <bruno@clisp.org>

build() {
  cd "${srcdir}/libunistring-${pkgver}"
  for _arch in ${_architectures}; do
    mkdir -p build-${_arch} && pushd build-${_arch}
    ${_arch}-configure \
      --enable-threads=win32
    make
    popd
  done
}

package() {
  for _arch in ${_architectures}; do
    cd "${srcdir}/libunistring-${pkgver}/build-${_arch}"
    make DESTDIR="${pkgdir}" install
    find "${pkgdir}/usr/${_arch}" -name '*.dll' -exec ${_arch}-strip --strip-unneeded {} \;
    find "${pkgdir}/usr/${_arch}" -name '*.a' -o -name '*.dll' | xargs ${_arch}-strip -g
    rm "${pkgdir}/usr/${_arch}/share/info/dir"
  done
}

# vim:set ts=2 sw=2 et:
