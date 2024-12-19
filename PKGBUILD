# Maintainer: Aleksana QwQ <me@aleksana.moe>

pkgname=npth
pkgver=1.8
pkgrel=1
pkgdesc='The new GNU portable threads library'
arch=(x86_64 aarch64 riscv64 loongarch64)
url="https://www.gnupg.org/software/npth/index.html"
license=('LGPL-2.1-or-later')
depends=('musl' 'sh')
provides=('libnpth.so')
source=("https://gnupg.org/ftp/gcrypt/${pkgname}/${pkgname}-${pkgver}.tar.bz2"
	"fix-musl-build.patch")
sha512sums=('34fdeea3d8a7a594d8fdbcc6d5d389b5c8e282e8e84c1491b1e51960c0fa007df6a1d62543f0107f0772f3215557d4b25c2a9c7067cb0ae2f8de7b4d63d09fb4'
            'a1019fcd7bcc276a1fda42c97cc41b14ed0130127966e3733c55235d830f095d9fe4f54cf91be52e6a5616860bbc1bc5f10c150c282987db8d83693725768542')

prepare()
{
  _patch_ "${pkgname}-${pkgver}"
  cd "${pkgname}-${pkgver}"
  autoreconf -fiv
}

build()
{
  cd "${pkgname}-${pkgver}"
  ./configure --prefix=/usr
  make
}

check()
{
  cd "${pkgname}-${pkgver}"
  make check
}

package()
{
  cd "${pkgname}-${pkgver}"
  make DESTDIR="${pkgdir}" install
  install -vDm 644 {README,NEWS,ChangeLog} \
    -t "${pkgdir}/usr/share/doc/${pkgname}"
}
