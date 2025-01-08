# Maintainer: Yukari Chiba <i@0x7f.cc>

pkgname=vulkan-headers
_pkgname=Vulkan-Headers
pkgver=1.4.303
pkgrel=1
pkgdesc="Vulkan header files"
arch=(any)
url="https://www.khronos.org/vulkan/"
license=('APACHE')
makedepends=(cmake ninja git)
source=("${pkgname}-${pkgver}.tar.gz::https://github.com/KhronosGroup/Vulkan-Headers/archive/v${pkgver}.tar.gz")
sha256sums=('fdf0e2e05356b455137ff97f837c9689ba253ec7d20f87ad81575b9bdbe7fdd4')

build() {
  cmake -G Ninja -B build -S ${_pkgname}-$pkgver \
    -DCMAKE_INSTALL_PREFIX=/usr \
    -DCMAKE_BUILD_TYPE=Release
  cmake --build build
}

package() {
  DESTDIR="${pkgdir}" cmake --install build
}
