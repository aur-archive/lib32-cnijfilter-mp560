# Maintainer: lorim <lorimz AT gmail DOT com>

pkgname=lib32-cnijfilter-mp560
pkgver=3.20
_pkgreview=1
pkgrel=7
pkgdesc="Canon IJ Printer Driver (MP560 series) (32-bit)"
url="http://software.canon-europe.com/products/0010756.asp"
arch=('x86_64')
license=('custom')
depends=('lib32-popt' 'lib32-gtk2>=2.8.0' 'lib32-libxml2>=2.6.24' 'ghostscript')
makedepends=('autoconf>=2.13' 'automake>=1.6' 'tar' 'make' 'gcc-multilib')
conflicts=('cnijfilter-common')
options=(!libtool)
install=cnijfilter-mp560.install
source=(http://gdlp01.c-wss.com/gds/7/0100002367/01/cnijfilter-source-${pkgver}-${_pkgreview}.tar.gz
	id.patch
	cups.patch
	libpng15.patch
	automake.patch)

build() {
  export CC="gcc -m32 -D_IPP_PRIVATE_STRUCTURES -ldl"

  cd ${srcdir}/cnijfilter-source-${pkgver}-${_pkgreview}
  patch -p1 -i ${srcdir}/id.patch
  patch -p1 -i ${srcdir}/cups.patch
  patch -p1 -i ${srcdir}/libpng15.patch
  patch -p1 -i ${srcdir}/automake.patch

  cd ${srcdir}/cnijfilter-source-${pkgver}-${_pkgreview}/libs
  ./autogen.sh --prefix=/usr --program-suffix=mp560 --libdir=/usr/lib32
  make

  cd ${srcdir}/cnijfilter-source-${pkgver}-${_pkgreview}/cngpij
  ./autogen.sh --prefix=/usr --program-suffix=mp560 --enable-progpath=/usr/bin --libdir=/usr/lib32
  make

  cd ${srcdir}/cnijfilter-source-${pkgver}-${_pkgreview}/cngpijmon
  ./autogen.sh --prefix=/usr --program-suffix=mp560 --enable-progpath=/usr/bin --libdir=/usr/lib32
  make

  cd ${srcdir}/cnijfilter-source-${pkgver}-${_pkgreview}/cnijfilter
  ./autogen.sh --prefix=/usr --program-suffix=mp560 --enable-progpath=/usr/bin --libdir=/usr/lib32
  make

  cd ${srcdir}/cnijfilter-source-${pkgver}-${_pkgreview}/pstocanonij
  ./autogen.sh --prefix=/usr --enable-progpath=/usr/bin --libdir=/usr/lib32
  sed -i 's:filterdir =.*$:filterdir = /usr/lib/cups/filter:g' filter/Makefile
  make

  cd ${srcdir}/cnijfilter-source-${pkgver}-${_pkgreview}/lgmon
  ./autogen.sh --prefix=/usr --program-suffix=mp560 --enable-progpath=/usr/bin --libdir=/usr/lib32
  make

  cd ${srcdir}/cnijfilter-source-${pkgver}-${_pkgreview}/backend
  ./autogen.sh --prefix=/usr --program-suffix=mp560 --enable-progpath=/usr/bin --libdir=/usr/lib32
  make

  cd ${srcdir}/cnijfilter-source-${pkgver}-${_pkgreview}/backendnet
  ./autogen.sh --prefix=/usr --program-suffix=mp560 --enable-progpath=/usr/bin --libdir=/usr/lib32
  make

  cd ${srcdir}/cnijfilter-source-${pkgver}-${_pkgreview}/cngpijmon/cnijnpr
  ./autogen.sh --prefix=/usr --program-suffix=mp560 --enable-progpath=/usr/bin --libdir=/usr/lib32
  make

  cd ${srcdir}/cnijfilter-source-${pkgver}-${_pkgreview}/printui
  ./autogen.sh --prefix=/usr --program-suffix=mp560 --enable-progpath=/usr/bin --libdir=/usr/lib32
  make

  cd ${srcdir}/cnijfilter-source-${pkgver}-${_pkgreview}/ppd
  ./autogen.sh --prefix=/usr --program-suffix=mp560
  make
}

package() {
  cd ${srcdir}/cnijfilter-source-${pkgver}-${_pkgreview}/libs
  make DESTDIR=${pkgdir} install

  cd ${srcdir}/cnijfilter-source-${pkgver}-${_pkgreview}/cngpij
  make DESTDIR=${pkgdir} install

  cd ${srcdir}/cnijfilter-source-${pkgver}-${_pkgreview}/cngpijmon
  make DESTDIR=${pkgdir} install

  cd ${srcdir}/cnijfilter-source-${pkgver}-${_pkgreview}/cnijfilter
  make DESTDIR=${pkgdir} install

  cd ${srcdir}/cnijfilter-source-${pkgver}-${_pkgreview}/pstocanonij
  make DESTDIR=${pkgdir} install

  cd ${srcdir}/cnijfilter-source-${pkgver}-${_pkgreview}/lgmon
  make DESTDIR=${pkgdir} install

  cd ${srcdir}/cnijfilter-source-${pkgver}-${_pkgreview}/backend
  make DESTDIR=${pkgdir} install

  cd ${srcdir}/cnijfilter-source-${pkgver}-${_pkgreview}/backendnet
  make DESTDIR=${pkgdir} install

  cd ${srcdir}/cnijfilter-source-${pkgver}-${_pkgreview}/cngpijmon/cnijnpr
  make DESTDIR=${pkgdir} install

  cd ${srcdir}/cnijfilter-source-${pkgver}-${_pkgreview}/printui
  make DESTDIR=${pkgdir} install

  cd ${srcdir}/cnijfilter-source-${pkgver}-${_pkgreview}/ppd
  make DESTDIR=${pkgdir} install

  cd ${srcdir}/cnijfilter-source-${pkgver}-${_pkgreview}
  install -d ${pkgdir}/usr/lib/bjlib
  install -m 755 360/database/* ${pkgdir}/usr/lib/bjlib
  install -d ${pkgdir}/usr/lib32
  install -s -m 755 360/libs_bin/*.so.* ${pkgdir}/usr/lib32
  install -s -m 755 com/libs_bin/*.so.* ${pkgdir}/usr/lib32
  install -D LICENSE-cnijfilter-${pkgver}EN.txt ${pkgdir}/usr/share/licenses/${pkgname}/LICENSE-cnijfilter-${pkgver}EN.txt

}

sha256sums=('2fc4dcd79d6644baeb0c8a0ee1b43dc9f59f44d21f773c0d85bfe2660a180b9a'
            '8edfc00b955895e9c4dbe1707ba700c8efee212a6b5fde46b80f2a92e5a0df38'
            '51cce3b50223b55513e4df00f78d55b4f9777c8b2e07243a589f6f9169eee78d'
            '03ca791dd57d6b64c7e79d0c98b45616ce9f0de4a432481728e1c52dbc96fd94'
            '3077b51e473a854920d5733a98be80fa2d6050588e7b7cf1800bdb2ea28bb6c8')
