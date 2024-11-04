# Maintainer: Yukari Chiba <i@0x7f.cc>

pkgname=utf8cpp
pkgver=4.0.6
pkgrel=1
pkgdesc="UTF-8 with C++ in a Portable Way"
arch=(any)
url="https://github.com/nemtrif/utfcpp"
license=(custom:BSL)
makedepends=(cmake)
source=(${url}/archive/v${pkgver}/${pkgname}-${pkgver}.tar.gz)
sha256sums=('6920a6a5d6a04b9a89b2a89af7132f8acefd46e0c2a7b190350539e9213816c0')

build() {
  cmake -B build -S ${pkgname/8}-${pkgver} \
    -DCMAKE_BUILD_TYPE=None \
    -DCMAKE_INSTALL_PREFIX=/usr \
    -DUTF8_TESTS=OFF
  make -C build
}

package() {
  make -C build DESTDIR="${pkgdir}" install
  install -Dm644 ${pkgname/8}-${pkgver}/LICENSE -t "${pkgdir}"/usr/share/licenses/${pkgname}/
}

