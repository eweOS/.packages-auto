# Maintainer: Yukari Chiba <i@0x7f.cc>

pkgname=xdg-desktop-portal
# 1.19.1 failed
# https://github.com/flatpak/xdg-desktop-portal/issues/1547
pkgver=1.19.1
pkgrel=1
pkgdesc="Desktop integration portals for sandboxed apps"
url="https://flatpak.github.io/xdg-desktop-portal/"
arch=(x86_64 aarch64 riscv64 loongarch64)
license=(LGPL)
depends=(
  geoclue
  glib
  json-glib
  pipewire
  fuse3
  gdk-pixbuf
  bubblewrap
  gstreamer-devel
)
makedepends=(
  docbook-xsl
  flatpak
  git
  libportal
  meson
  xmlto
  python-packaging
)
optdepends=('xdg-desktop-portal-impl: Portal backends')
source=("git+https://github.com/flatpak/xdg-desktop-portal#tag=$pkgver")
sha256sums=('9b03626ec1a1f6ca2f89aff314b2449465d2cd2176aecf8d7915804891664fa9')

prepare() {
  _patch_ $pkgname
}

build() {
  local features=(
    -D documentation=disabled	# missing python-sphinx
    -D systemd=disabled
    -D man-pages=disabled
    -D pytest=disabled
  )
  ewe-meson $pkgname build "${features[@]}"
  meson compile -C build
}

# missing umockdev, requires gudev
#check() {
#  meson test -C build --print-errorlogs
#}

package() {
  meson install -C build --destdir "$pkgdir"

  # remove systemd services
  rm -r $pkgdir/usr/lib/systemd || true
}
