# Maintainer: Yukari Chiba <i@0x7f.cc>

pkgname=python-wrapt
pkgver=1.17.0
pkgrel=1
pkgdesc="A Python module for decorators, wrappers and monkey patching"
arch=(x86_64 aarch64 riscv64 loongarch64)
url="https://pypi.python.org/pypi/wrapt"
license=("BSD-2-Clause")
depends=('python')
makedepends=('python-build' 'python-installer' 'python-setuptools' 'python-wheel')
checkdepends=('python-pytest')
source=("https://github.com/GrahamDumpleton/wrapt/archive/refs/tags/${pkgver}.tar.gz" fix-py313-test.patch)
sha512sums=('b552676a9c41c2feadf9eeab78c011bcc068f6b160d5d91aa6afc8b880abaaf8f170071e8eb03811959d3510cb19cb8fcc0db41a3c4e7eb6c92cf04882d9c0d2'
            '0aaa87158e43ac6cca432634ad806675f6c3bbe017118bbbe4ed801b0f0d711dc6f1e69a14f5b663d57e9fbf11036faec3d9f5fd33fed860b6c2e142c02687b3')

prepare() {
  _patch_ wrapt-$pkgver
}

build() {
  cd wrapt-$pkgver
  python -m build --wheel --no-isolation
}

check() {
  local python_version=$(python -c 'import sys; print("".join(map(str, sys.version_info[:2])))')

  cd wrapt-$pkgver
  PYTHONPATH="$PWD/build/lib.linux-$CARCH-cpython-$python_version" py.test
}

package() {
  cd wrapt-$pkgver
  python -m installer --destdir="$pkgdir" dist/*.whl
  install -Dm644 LICENSE "$pkgdir"/usr/share/licenses/$pkgname/LICENSE
}
