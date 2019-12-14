# Maintainer: Andreas Radke <andyrtr@archlinux.org>
# Maintainer: Jan de Groot <jgc@archlinux.org>
# Patches added by Katie Jones.

pkgname=xkeyboard-config-f13
_pkgname=xkeyboard-config
pkgver=2.28
pkgrel=1
pkgdesc="X keyboard configuration files"
arch=(any)
license=('custom')
url="https://www.freedesktop.org/wiki/Software/XKeyboardConfig"
makedepends=('intltool' 'xorg-xkbcomp' 'libxslt')
provides=('xkbdata' 'xkeyboard-config')
replaces=('xkbdata' 'xkeyboard-config')
conflicts=('xkbdata' 'xkeyboard-config')
source=(https://xorg.freedesktop.org/archive/individual/data/${_pkgname}/${_pkgname}-${pkgver}.tar.bz2{,.sig}
    'kj.patch')
validpgpkeys=('FFB4CCD275AAA422F5F9808E0661D98FC933A145')
validpgpkeys+=('15CFA5C595041D2CCBEA155F1732AA424A0E86B4') # "Sergey Udaltsov (For GNOME-related tasks) <svu@gnome.org>"
sha512sums=('be38e61a7d3a1c03f9dc92fed5aada65fdb8b42272e874e01156a39de07f2a7c81846e9ba449aeb95661587f8d05217d549a1315ee0dd92facbb6158362e68ae'
            'SKIP'
        'SKIP')

build() {
  cd ${_pkgname}-${pkgver}

  patch -p1 < "${srcdir}/kj.patch"

  ./configure --prefix=/usr \
      --with-xkb-base=/usr/share/X11/xkb \
      --with-xkb-rules-symlink=xorg \
      --enable-compat-rules=yes
  make
 }
 
 package() { 
  cd ${_pkgname}-${pkgver}

  make DESTDIR="${pkgdir}" install
  rm -f "${pkgdir}/usr/share/X11/xkb/compiled"

  install -m755 -d "${pkgdir}/var/lib/xkb"
  install -m755 -d "${pkgdir}/usr/share/licenses/${_pkgname}"
  install -m644 COPYING "${pkgdir}/usr/share/licenses/${_pkgname}/"
}
