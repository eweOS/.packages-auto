# Maintainer: Yukari Chiba <i@0x7f.cc>

pkgname=python-markupsafe
pkgver=3.0.2
pkgrel=1
pkgdesc="Implements a XML/HTML/XHTML Markup safe string for Python"
arch=(x86_64 aarch64 riscv64 loongarch64)
url="https://pypi.python.org/pypi/MarkupSafe"
license=('BSD-3-Clause')
depends=('python')
makedepends=('git' 'python-build' 'python-installer' 'python-setuptools' 'python-wheel')
checkdepends=('python-pytest')
source=("git+https://github.com/pallets/markupsafe.git#tag=$pkgver")
sha512sums=('4e2fb5b69fd993784c965804037a62963cc64729d20c473c941e2ed238fe6ae5e7a2610d2678db908bf3e2b05c334d17e79d2476c3e147541b38f3270622f77f')

build() {
  cd markupsafe
  python -m build --wheel --no-isolation
}

check() {
  cd markupsafe
  PYTHONPATH=src pytest
}

package() {
  cd markupsafe
  python -m installer --destdir="$pkgdir" dist/*.whl
  install -Dm644 LICENSE.rst -t "$pkgdir"/usr/share/licenses/$pkgname/
}
