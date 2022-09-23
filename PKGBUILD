# Maintainer: Yukari Chiba <i@0x7f.cc>

pkgname=rust
pkgver=1.64.0
pkgrel=1
pkgdesc="Systems programming language focused on safety, speed and concurrency"
arch=('x86_64')
url='https://www.rust-lang.org/'
license=(MIT Apache)
source=(
    https://static.rust-lang.org/dist/rustc-1.64.0-src.tar.gz
    https://sh.rustup.rs/rustup-init.sh
    config.toml
)
sha256sums=('SKIP' 'SKIP' 'SKIP')

depends=(musl llvm-libs musl-static curl libssh2)
makedepends=(rust llvm libffi perl python cmake ninja)

prepare() {
  chmod +x rustup-init.sh
  ./rustup-init.sh --profile minimal -y
  source "$HOME/.cargo/env"

  cp config.toml ${pkgname}c-${pkgver}-src/
}

build() {
  source "$HOME/.cargo/env"
  
  cd ${pkgname}c-${pkgver}-src

  export RUST_BACKTRACE=1
  
  DESTDIR="$srcdir/install" python ./x.py install -j "$(nproc)"
}

package() {
  provides=(cargo rustfmt)
  cp -r $srcdir/install/* "$pkgdir"

  rm $pkgdir/usr/lib/rustlib/{components,install.log,rust-installer-version,uninstall.sh}
  rm $pkgdir/usr/lib/rustlib/manifest-*

  install -d $pkgdir/usr/share/bash-completion
  install -d $pkgdir/usr/share/licenses/rust
  mv $pkgdir/etc/bash_completion.d $pkgdir/usr/share/bash-completion/completions
  mv -t $pkgdir/usr/share/licenses/rust $pkgdir/usr/share/doc/rust/{COPYRIGHT,LICENSE*}
}
