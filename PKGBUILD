# Maintainer: Yukari Chiba <i@0x7f.cc>

pkgname=limine
pkgver=8.5.0
pkgrel=1
pkgdesc="An advanced, portable, multiprotocol bootloader"
arch=(x86_64 aarch64 riscv64 loongarch64)
url="https://limine-bootloader.org/"
license=('BSD')
makedepends=('nasm' 'lld' 'mtools')
optdepends=('efibootmgr: efi entries managing for limine-install')
source=(
  "https://github.com/limine-bootloader/limine/releases/download/v${pkgver}/${pkgname}-${pkgver}.tar.gz"
  limine-mkconfig
  limine.defaults
  limine.conf
  limine-install
)
sha256sums=('e912eef6e78521c904253b3d87e995f2c8267cfda3add0635ff927cf60c44d1a'
            '7952ba8555a3b82725cd8f7255a91f8cf363e8cfd99d86aa7438638252239665'
            'b1d39bd3cc56b4d033f2ffe3c6f1eda8cbb0eb4788626e5041fcb56fa961ea86'
            'f722aacb1e5865489483c14b950900998241fe6558e58875b1119579ef91a5e0'
            '996416f738c981e2d04af00407adb7bc1e95a5acc5b11f65595d202cd6420290')

build() {
  cd "${pkgname}-${pkgver}"
  local target_options=(
    --enable-uefi-$CARCH
    --enable-uefi-cd
  )
  [ $CARCH = x86_64 ] && target_options+=(--enable-bios --enable-bios-cd --enable-bios-pxe)
  ./configure --prefix=/usr ${target_options[*]} TOOLCHAIN_FOR_TARGET=llvm
  make
}

package() {
  cd "${pkgname}-${pkgver}"
  make DESTDIR="${pkgdir}" install
  install -Dm 644 COPYING "${pkgdir}/usr/share/licenses/${pkgname}/COPYING"
  install -Dm 755 $srcdir/limine-mkconfig "$pkgdir/usr/bin/limine-mkconfig"
  install -Dm 755 $srcdir/limine-install "$pkgdir/usr/bin/limine-install"
  install -Dm 644 $srcdir/limine.defaults "$pkgdir/etc/default/limine"
  install -Dm 644 $srcdir/limine.conf "$pkgdir/etc/limine.conf"
}

