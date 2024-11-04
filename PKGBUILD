# Maintainer: Aleksana QwQ <me@aleksana.moe>
# Contributor: Sergej Pupykin <pupykin.s+arch@gmail.com>
# Contributor: Gerardo Exequiel Pozzi <vmlinuz386@yahoo.com.ar>

pkgname=chrpath
pkgver=0.18
pkgrel=1
pkgdesc="Change or delete the rpath or runpath in ELF files"
arch=(x86_64 aarch64 riscv64 loongarch64)
url="https://directory.fsf.org/project/chrpath/"
license=('GPL2')
depends=('musl')
source=("http://http.debian.net/debian/pool/main/c/chrpath/chrpath_$pkgver.orig.tar.gz")
sha256sums=('f09c49f0618660ca11fc6d9580ddde904c7224d4c6d0f6f2d1f9bcdc9102c9aa')

prepare()
{
  cd "${srcdir}"/$pkgname-$pkgver
  autoreconf -fiv
}

build()
{
  cd "${srcdir}"/$pkgname-$pkgver
  ./configure --prefix=/usr --mandir=/usr/share/man
  make
}

package()
{
  cd "${srcdir}"/$pkgname-$pkgver
  make DESTDIR="${pkgdir}" docdir=/usr/share/doc/chrpath install
}
