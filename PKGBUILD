# Maintainer: Yukari Chiba <i@0x7f.cc>

pkgname=libcap
pkgver=2.72
pkgrel=1
pkgdesc="POSIX 1003.1e capabilities"
arch=(x86_64 aarch64 riscv64 loongarch64)
url="https://sites.google.com/site/fullycapable/"
license=(GPL-2.0-only)
makedepends=(linux-headers)
source=(https://kernel.org/pub/linux/libs/security/linux-privs/${pkgname}2/$pkgname-$pkgver.tar.xz)
sha256sums=('0274f5a15a5205f656d8f0169eef711dd29158ba8ad3b240618b342b2460175b')

build()
{
  make \
    HOSTCC=clang CC=clang \
    DYNAMIC=yes KERNEL_HEADERS=/usr/include \
    lib=lib prefix=/usr sbindir=bin \
    -C $pkgname-$pkgver
}

package()
{
  make HOSTCC=clang CC=clang \
    DESTDIR="$pkgdir" \
    RAISE_SETFCAP=no \
    lib=lib prefix=/usr sbindir=bin \
    install -C $pkgname-$pkgver
}
