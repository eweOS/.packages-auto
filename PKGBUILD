# Maintainer: Yukari Chiba <i@0x7f.cc>

pkgname=gnome-terminal
pkgver=3.54.0
pkgrel=1
pkgdesc="The GNOME Terminal Emulator"
url="https://wiki.gnome.org/Apps/Terminal"
arch=(x86_64 aarch64 riscv64)
license=(
  # Program
  GPL-3.0-or-later

  # Documentation
  CC-BY-SA-3.0
  GPL-3.0-only

  # Appstream-data
  GFDL-1.3-only
)
depends=(
  dconf
  glib2
  gsettings-desktop-schemas
  gtk3
  hicolor-icon-theme
  libhandy
  pango
  util-linux-libs
  vte3
)
makedepends=(
  docbook-xsl
  git
  glib2
  meson
  yelp-tools
)
optdepends=(
  "libnautilus-extension: Nautilus integration"
)
groups=(gnome-extra)
source=("git+https://gitlab.gnome.org/GNOME/gnome-terminal.git#tag=$pkgver" fix-W_EXITCODE.patch)
sha256sums=('05021a11012e6d5191177a7a41adb8dc4060cb3bf1d21cdfe0e5a1eee77db0ad'
            '534cd9e39421732e13b198c02734b433c7d2d35e41109b6deea8516bacf0e636')

prepare() {
  _patch_ $pkgname
}

build() {
  local meson_options=(
    -D b_lto=false
    -D nautilus_extension=false
  )

  ewe-meson $pkgname build "${meson_options[@]}"
  meson compile -C build
}

check() {
  meson test -C build --print-errorlogs
}

package() {
  meson install -C build --destdir "$pkgdir"
  
  # FIXME: terminal server
  rm -r $pkgdir/usr/lib/systemd
}
