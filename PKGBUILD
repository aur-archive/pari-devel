# $Id: PKGBUILD 128041 2015-02-20 17:54:31Z bisson $
# Maintainer: Gaetan Bisson <bisson@archlinux.org>

pkgname=pari-devel
_pkgver=2.8-1369-g0e48e9b
pkgver=${_pkgver//-/.}
pkgrel=1
pkgdesc='Computer algebra system designed for fast computations in number theory. Development snapshot'
url='http://pari.math.u-bordeaux.fr/'
license=('GPL')
arch=('i686' 'x86_64')
depends=('gmp' 'readline' 'libx11')
makedepends=('perl' 'texlive-core')
optdepends=('perl: gphelp, tex2mail')
conflicts=('pari')
provides=('pari')
source=("http://www.sagemath.org/packages/upstream/pari/pari-$_pkgver.tar.gz" 'public_memory_functions.patch')
md5sums=('2ae5684a10d557016fc1b6ad10b8bf80'
         '9172b9faee975cd3fe0f97126ea61af8')

prepare() {
	cd pari-${_pkgver}
	sed 's/\$addlib64//g' -i config/get_libpth

# make some private functions public
  patch -p1 -i "$srcdir"/public_memory_functions.patch
}

build() {
	cd pari-${_pkgver}
	./Configure \
		--prefix=/usr \
		--with-readline \
		--mt=pthread \
		--with-gmp \

	make all
}

package() {
	cd pari-${_pkgver}
	make DESTDIR="${pkgdir}" install
	ln -sf gp.1.gz "${pkgdir}"/usr/share/man/man1/pari.1
}
