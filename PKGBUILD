# Maintainer: Yukari Chiba <i@0x7f.cc>

pkgname=python-jinja
_name="${pkgname#python-}"
pkgver=3.1.5
pkgrel=1
pkgdesc="A simple pythonic template language written in Python"
arch=('any')
url="https://palletsprojects.com/p/jinja/"
license=('BSD-3-Clause')
depends=('python' 'python-markupsafe')
makedepends=('python-build' 'python-installer' 'python-setuptools' 'python-wheel' 'python-flit-core')
optdepends=('python-babel: for i18n support')
#checkdepends=('python-pytest' 'python-trio')
source=($_name-$pkgver.tar.gz::https://github.com/pallets/jinja/archive/refs/tags/$pkgver.tar.gz python3.13.patch)
sha256sums=('684d78790cc747f4b4b68b365783af8cac770c2c66d9f414b21c8b8480e019d0'
            '084466f1d3db4cf51336b8a01e6260624960f0f73de701c54f7890d1dd540d6d')

prepare() {
  _patch_ $_name-$pkgver
}

build() {
  cd $_name-$pkgver
  python -m build --wheel --no-isolation
}

check() {
  cd $_name-$pkgver
  #FIXME: missing dependency python-trio
  #PYTHONPATH=src pytest
}

package() {
  cd $_name-$pkgver
  python -m installer -d "$pkgdir" dist/*.whl
  install -Dm644 LICENSE.txt -t "$pkgdir/usr/share/licenses/$pkgname"
}
