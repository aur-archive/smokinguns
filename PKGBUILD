# Maintainer leper <blubblub@mail.ru>

pkgname=smokinguns
pkgver=1.1
pkgrel=8
pkgdesc='A semi-realistic simulation of the "old west" great atmosphere built on id Tech 3.'
url="http://www.smokin-guns.org"
arch=('i686' 'x86_64')
license=('GPL2')
depends=('sdl' 'openal' 'curl' 'libjpeg' 'speex' 'libgl' 'glu' 'alsa-lib' 'smokinguns-data')
conflicts=('smokinguns-bin')
source=("https://github.com/smokin-guns/SmokinGuns/archive/v${pkgver}.tar.gz"
        "$pkgname.desktop"
        'x86_64.patch')
md5sums=('b97a54ded330eee05a4ec163ec10def4'
         'c0622e33e16efbd67af1b1c92c4be2e6'
         'a7b8c389b9964f645e05254f08981f46')

prepare() {
  cd "$srcdir/SmokinGuns-$pkgver"

  # Fix build on x86_64 (backported from ioquake3 trunk)
  if [ "$CARCH" == "x86_64" ] ; then
    patch -p1 --remove-empty-files < "$srcdir/x86_64.patch"
  fi

  # Set basedir
  echo "DEFAULT_BASEDIR = /usr/share/$pkgname" >> "Makefile.local"
  # Use system libraries
  echo "USE_INTERNAL_ZLIB=0" >> "Makefile.local"
  echo "USE_INTERNAL_JPEG=0" >> "Makefile.local"
  echo "USE_INTERNAL_SPEEX=0" >> "Makefile.local"
  # Use system headers
  echo "USE_LOCAL_HEADERS=0" >> "Makefile.local"
}

build() {
  cd "$srcdir/SmokinGuns-$pkgver"
  make
}

package() {
  cd "$srcdir/SmokinGuns-$pkgver"

  SUFFIX=${CARCH//i686/i386}
  install -Dm 755 "build/release-linux-${SUFFIX}/$pkgname.${SUFFIX}" "$pkgdir/usr/bin/$pkgname"
  install -Dm 755 "build/release-linux-${SUFFIX}/${pkgname}_dedicated.${SUFFIX}" "$pkgdir/usr/bin/${pkgname}_dedicated"

  install -Dm 644 "$srcdir/$pkgname.desktop" "$pkgdir/usr/share/applications/$pkgname.desktop"
  install -Dm 644 "misc/$pkgname.png" "$pkgdir/usr/share/pixmaps/$pkgname.png"
}

# vim:set ts=2 sw=2 et:
