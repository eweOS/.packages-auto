# Maintainer: Yukari Chiba <i@0x7f.cc>

pkgname=pango
pkgver=1.55.5
pkgrel=1
pkgdesc="A library for layout and rendering of text"
url="https://www.pango.org/"
arch=(x86_64 aarch64 riscv64 loongarch64)
license=(LGPL)
depends=(cairo glib fribidi harfbuzz)
makedepends=(meson gobject-introspection)
provides=(libpango-1.0.so libpangocairo-1.0.so libpangoft2-1.0.so)
source=("https://gitlab.gnome.org/GNOME/$pkgname/-/archive/$pkgver/$pkgname-$pkgver.tar.gz")
sha256sums=('889bd6d3472e3013f89a6435d9f718540c92ce0dc3a9154189a010426bc4ffa7')

build() {
  ewe-meson $pkgname-$pkgver build \
    -D libthai=disabled \
    -D xft=disabled
  meson compile -C build
}

package() {
  meson install -C build --destdir "$pkgdir"
}

