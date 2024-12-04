# Maintainer: Yukari Chiba <i@0x7f.cc>

pkgname=python-jinja
_name="${pkgname#python-}"
pkgver=3.1.4
pkgrel=2
pkgdesc="A simple pythonic template language written in Python"
arch=('any')
url="https://palletsprojects.com/p/jinja/"
license=('BSD-3-Clause')
depends=('python' 'python-markupsafe')
makedepends=('python-build' 'python-installer' 'python-setuptools' 'python-wheel' 'python-flit-core')
optdepends=('python-babel: for i18n support')
#checkdepends=('python-pytest' 'python-trio')
source=($_name-$pkgver.tar.gz::https://github.com/pallets/jinja/archive/refs/tags/$pkgver.tar.gz python3.13.patch)
sha256sums=('ed06f67abd2c8b7697dfb714f80715903ab0507e3c5acc11e92477e4ea51033b'
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
