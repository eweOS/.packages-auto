# Maintainer: Yukari Chiba <i@0x7f.cc>

pkgname=mpd
pkgver=0.23.16
pkgrel=1
pkgdesc="Flexible, powerful, server-side application for playing music"
arch=(x86_64 aarch64 riscv64 loongarch64)
url="https://www.musicpd.org/"
license=(
  BSD-2-Clause
  GPL-2.0-or-later
)
depends=(
  hicolor-icon-theme
  pcre2
  zlib
  zziplib
)
makedepends=(
  alsa-lib
  boost
  bzip2
  curl
  dbus
  expat
  ffmpeg
  flac
  fluidsynth
  fmt
  git
  icu
  lame
  libmpdclient
  libogg
  libpulse
  libsamplerate
  libsndfile
  libvorbis
  linux-headers
  meson
  openal
  pipewire
  sqlite
)
backup=(etc/$pkgname.conf)
source=(
  $pkgname::git+https://github.com/MusicPlayerDaemon/MPD.git#tag=v${pkgver}
  $pkgname.conf
  $pkgname.sysusers
  $pkgname.tmpfiles
  $pkgname.service
  fmt11.patch
  back_inserter.patch
  icu76.patch
)
sha512sums=('87189e476a562e4e9f28596b221151260c9c42d6abc7198fce0eb2f7e670bd346282609bd196e4dd8179d1216e2c7ea5cf4d50b1eef459d54782089dec5c9888'
            '00be5ce1b167492946e049c66de472a482ff1e1c8939f6029626ff842f6370f1b7a046958a8ae58d56eb9eb192a05448fcb2ec072fe8614a836ee9e9df4dd027'
            '88ba2b6624e7dddd13a51e6fb9c7a65226d0c5b0645183901d6434c23fa0aca605989be0c600f2197c99c1b4c64396477aa15ab3c427087e86bb652977428aae'
            'f0ea57836f575dec93b12afb6c730c706b8745d25811152960dcd1f079760c2adda0b8af8e16e8329cc073c3b4e00edbbeea959ec6e1f5003ea77b0b6478262a'
            'a31e985fec72d16b52f1f2f1872a3a39e53addf387bcbb0792ece619e9dd2053a6646594e7d8f137de706ac65d80ba45ceef7a2a86f6cb0a49f17842aba98670'
            'dbafa218b176dcfefdb7eb77924d334e99a5db01ff8b75c965b09adbcca7e9d83483961aad5aa723623b7137a62d03021eaa3d6a1882b3ca463d7198b76f4e3b'
            '8b2618202101fef6ba9d69ffe641a66d83f22a678ebd9d474327274fbb5ffdc21497fdf69504425943a66af55d5a77d736f62dcc55f50eca2c4aa99c8d3bd92b'
            '02a6c97fcdb4dc637addaa7121a2446fd6e42417be36ab0a6213cb8d1c3a758f2f4605d3a483e077d7516b8bcb8f10c8bb759e0e11c82ad8568d181f4f7c3e91')

prepare() {
  _patch_ $pkgname
}

build() {
  local _disabled_comps=(
    adplug shine tremor io_uring chromaprint yajl id3tag cdio_paranoia mms
    qobuz iso9660 ao jack shout audiofile faad gme mad mikmod modplug
    openmpt mpcdec mpg123 wavpack wildmidi sidplay twolame soundcloud
    libmpdclient nfs
  )
  
  # NOTE: sndio conflicts with alsa
  # NOTE: nfs: field has incomplete type 'struct timeval'
  local _meson_options=(
    -D documentation=disabled
    -D sndio=disabled
    -D systemd=disabled
    -D b_ndebug=true
  )
  
  for _disabled_comp in "${_disabled_comps[@]}"; do
    _meson_options+=(-D ${_disabled_comp}=disabled)
  done

  ewe-meson "${_meson_options[@]}" build $pkgname
  ninja -C build
}

check() {
  ninja -C build test
}

package() {
  depends+=(
    alsa-lib libasound.so
    bzip2 libbz2.so
    curl libcurl.so
    dbus libdbus-1.so
    expat libexpat.so
    ffmpeg libav{codec,filter,format,util}.so
    flac libFLAC.so
    fluidsynth libfluidsynth.so
    fmt libfmt.so 
    icu libicui18n.so libicuuc.so
    lame libmp3lame.so
    libogg libogg.so
    pipewire
    libmpdclient libmpdclient.so
    libpulse libpulse.so
    libsamplerate libsamplerate.so
    libsndfile libsndfile.so
    libvorbis libvorbis{,enc}.so
    openal libopenal.so
    sqlite libsqlite3.so
  )

  DESTDIR="$pkgdir" ninja -C build install
  install -vDm 644 $pkgname/doc/${pkgname}conf.example -t "$pkgdir/usr/share/doc/$pkgname/"
  # NOTE: BSD-2-Clause license file currently missing: https://github.com/MusicPlayerDaemon/MPD/issues/1877
  # install -vDm 644 $pkgname-$pkgver/LICENSES/BSD-2-Clause -t "$pkgdir/usr/share/licenses/$pkgname/"
  install -vDm 644 $pkgname.conf -t "$pkgdir/etc/"
  install -vDm 644 $pkgname.sysusers "$pkgdir/usr/lib/sysusers.d/$pkgname.conf"
  install -vDm 644 $pkgname.tmpfiles "$pkgdir/usr/lib/tmpfiles.d/$pkgname.conf"
}
