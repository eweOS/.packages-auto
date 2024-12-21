# Maintainer: Yukari Chiba <i@0x7f.cc>

pkgname=nodejs
pkgver=23.5.0
pkgrel=1
pkgdesc='Evented I/O for V8 javascript'
arch=(x86_64 aarch64 riscv64 loongarch64)
url='https://nodejs.org/'
license=('MIT')
depends=('brotli' 'openssl' 'zlib' 'icu' 'libuv' 'libnghttp2' 'c-ares')
makedepends=('git' 'python' 'linux-headers')
#source=("git+https://github.com/nodejs/node.git#tag=v$pkgver")
source=("https://mirrors.tuna.tsinghua.edu.cn/nodejs-release/v${pkgver}/node-v${pkgver}.tar.xz" "fix-rv.patch")
sha512sums=('9fd5d17c5308021e70db7d570524fe430c049e10c481a319f0e38f0b91de74556bac1c146bfb0484bbe4c49ba8ed59019175c6c51da2b67a80d98dfdfe7cf298'
            'a06423d47ccfd7682c73559dc82ee787024daa0ac0d04b0f8a2c49238e99652242ed2f128dc4c7bf44d661abeb7679c289ed7cc1ecb1d9e576bd76738cad197d')

prepare() {
  _patch_ node-v$pkgver
  cd node-v$pkgver
  # Clang with libc++
  sed -i 's/-latomic//g' node.gyp
  sed -i 's/-latomic//g' tools/v8_gypfiles/v8.gyp
}

build() {
  cd node-v$pkgver
  export CC=cc CXX=c++
  ./configure \
    --prefix=/usr \
    --with-intl=system-icu \
    --without-npm \
    --shared \
    --shared-openssl \
    --shared-zlib \
    --shared-libuv \
    --experimental-http-parser \
    --shared-nghttp2 \
    --shared-cares \
    --shared-brotli

  make
}

check() {
  cd node-v$pkgver
  make test || :
}

package() {
  cd node-v$pkgver
  make DESTDIR="$pkgdir" install
  install -Dm644 LICENSE -t "$pkgdir"/usr/share/licenses/nodejs/

  cd "$pkgdir"/usr/lib
  ln -s libnode.so.* libnode.so
}
