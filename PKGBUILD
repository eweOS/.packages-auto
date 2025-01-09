# Maintainer: Yao Zi <ziyao@disroot.org>

pkgname=python-psutil
_pyname=${pkgname#*-}
pkgver=6.1.1
pkgrel=1
pkgdesc='Cross-platform lib for process and system monitoring in Python'
url='https://github.com/giampaolo/psutil'
arch=(x86_64 aarch64 riscv64 loongarch64)
license=(BSD-3-Clause)
depends=(python)
makedepends=(python-build python-installer python-setuptools python-wheel
	     linux-headers)
checkdepends=(python-pytest)
source=("https://github.com/giampaolo/psutil/archive/refs/tags/release-$pkgver.tar.gz")
sha256sums=('8a3fad3310797351aafe6bc5872cb4795f0879ba88fc92680658293c4712befd')

build () {
	cd $_pyname-release-$pkgver
	python -m build --wheel --no-isolation
}

package() {
	cd $_pyname-release-$pkgver
	python -m installer --destdir $pkgdir dist/*.whl
}
