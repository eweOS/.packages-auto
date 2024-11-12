# Maintainer: Yukari Chiba <i@0x7f.cc>

pkgname=neatvnc
pkgver=0.8.1
pkgrel=3
pkgdesc='Fast and neat VNC server library'
arch=(x86_64 aarch64 riscv64 loongarch64)
url=https://github.com/any1/neatvnc
license=(custom:ISC)
depends=(
  libaml.so
  libavcodec.so
  libdrm
  libpixman-1.so
  libturbojpeg.so
  mesa
  zlib
  nettle
)
makedepends=(
  git
  linux-headers
  meson
  ninja
)
provides=(libneatvnc.so)
source=(git+https://github.com/any1/neatvnc.git#tag=v$pkgver ffmpeg-7.1.patch)
sha256sums=('57a3a0a2469b93acf2a3afad2feb703cc7542b75c3e52de04d8d589549f79da7'
            '56281ca07173b9b30862d0a00e543c3599f9a22f04112666f3dbd76bff495c8d')

prepare() {
  _patch_ neatvnc
}

build() {
  ewe-meson neatvnc build -D tls=disabled
  meson compile -C build
}

package() {
  DESTDIR="${pkgdir}" meson install -C build
  install -Dm 644 neatvnc/COPYING -t "${pkgdir}"/usr/share/licenses/neatvnc
}
