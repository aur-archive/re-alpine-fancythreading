# $Id$
# Maintainer: Mark Pustjens <pustjens@dds.nl>
# Contributor:  Eric Bélanger <eric@archlinux.org>
# Contributor: Smith Dhumbumroong <zodmaner@gmail.com>

pkgname=re-alpine-fancythreading
real_pkgname=re-alpine
pkgver=2.03
pkgrel=1
pkgdesc="The continuation of the Alpine email client from University of Washington. Including Enhanced fancy threading and Topal patches."
arch=('i686' 'x86_64')
url="http://sourceforge.net/projects/re-alpine/"
license=('APACHE')
depends=('libldap' 'krb5')
optdepends=('aspell: spell-checking support'
	    'hunspell: spell-checking support')
provides=('pine' 'alpine')
conflicts=('pine' 'alpine' 're-alpine')
replaces=('pine' 'alpine')
options=('!makeflags')
source=(http://downloads.sourceforge.net/project/re-alpine/${real_pkgname}-${pkgver}.tar.bz2 
        maildir.patch
	fancy.patch 
	alpine-2.02.patch-1
	alpine-2.00.patch-2
	misc-compile.patch)
sha1sums=('8e1c4f4a4d38814478e8bd3bbeed1c0f8ee9491b'
          'c09a8e42f9dba3e63a3755a9c418af95da721d8d'
          'cac10cf4c92d290e5f3bc0946050649bd9172fb9'
          '95d2099637ff21fa45745b9390509543a048561a'
          'ab91faac11c045f8d85002a7c286113be5247fd3'
          '7708d22f7ad00200535b48b2ceb9e2d052cd20ee')

build() {
  cd "${srcdir}/${real_pkgname}-${pkgver}"
  patch -p1 -i "${srcdir}/fancy.patch"
  patch -p1 -i "${srcdir}/maildir.patch"
  patch -p1 -i "${srcdir}/alpine-2.02.patch-1"
  patch -p1 -i "${srcdir}/alpine-2.00.patch-2"
  patch -p1 -i "${srcdir}/misc-compile.patch"
   LIBS+="-lpam -lkrb5 -lcrypto" ./configure --prefix=/usr --with-passfile=.pine-passfile --without-tcl \
    --disable-shared --with-system-pinerc=/etc/alpine.d/pine.conf \
    --with-system-fixed-pinerc=/etc/alpine.d/pine.conf.fixed
  make
}

package() {
  cd "${srcdir}/${real_pkgname}-${pkgver}"
  make DESTDIR="${pkgdir}" install
}
