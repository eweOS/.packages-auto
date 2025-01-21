# Maintainer: Yukari Chiba <i@0x7f.cc>

pkgname=lxqt-runner
pkgver=2.1.1
pkgrel=1
pkgdesc="The LXQt application launcher"
arch=("x86_64" "aarch64" "riscv64" "loongarch64")
groups=("lxqt")
url="https://github.com/lxqt/$pkgname"
license=("LGPL2.1")
depends=("lxqt-globalkeys" "muparser" "libQt6Xdg.so" "layer-shell-qt")
makedepends=("lxqt-build-tools")
source=(
	"https://github.com/lxqt/$pkgname/releases/download/$pkgver/$pkgname-$pkgver.tar.xz"
    no-x11.patch
)
sha256sums=('bc764f027bcd3e40d5fa3c28b31db975aa8c1f5f75218384c5b1b3b37f8cbb5e'
            'fa7716cbdf651319d4d655ff063354a1b5f0554f43f8590829335e294a27d5b7')

prepare() {
  _patch_ $pkgname-$pkgver
}

build() {
	cmake -B build -S "$srcdir/$pkgname-$pkgver" \
		-DCMAKE_BUILD_TYPE=None \
		-DCMAKE_INSTALL_PREFIX=/usr
	make -C build
}

package() {
	cd build
	make DESTDIR="$pkgdir" install
}
