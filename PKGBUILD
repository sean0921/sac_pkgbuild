# Contributor: Sean Ho <sean.li.shin.ho@gmail.com>

pkgname=sac-iris
_pkgname=sac
pkgver=101.6a
pkgrel=2
pkgdesc="The Seismic Analysis Code (SAC) is one of the most widely used analysis packages for regional and teleseismic seismic data."
arch=(x86_64)
url="http://ds.iris.edu/ds/nodes/dmc/forms/sac/"
license=('custom')
depends=('libx11' 'ncurses' 'readline')
source=("local://sac-${pkgver}-source.tar.gz")
sha256sums=('10e718c78cbbed405cce5b61053f511c670a85d986ee81d45741f38fcf6b57d5')

prepare() {
  cd "${srcdir}/${_pkgname}-${pkgver}"
  patch -p1 < ../../0001-Fix-missing-DESTDIR-variable-in-Makefile.patch
  patch -p1 < ../../0002-correct-name-of-autoreconf-file-configure.ac.patch
  patch -p1 < ../../0003-correct-automake-variable-syntax.patch
  rm -vf bin/sac-config bin/sacinit.csh bin/sacinit.sh
  cd "${srcdir}/${_pkgname}-${pkgver}"
  autoreconf -fiv
  ./configure CFLAGS="-fcommon" --prefix /opt/sac/ --enable-readline
}

build() {
  cd "${srcdir}/${_pkgname}-${pkgver}"
  make || return 1
}

package() {
  mkdir -pv "${pkgdir}"/usr/bin/
  mkdir -pv "${pkgdir}"/etc/profile.d/
  cd "${srcdir}/${_pkgname}-${pkgver}"
  make DESTDIR="${pkgdir}" install || return 1
  ln -rsv "${pkgdir}"/opt/sac/bin/sac "${pkgdir}"/usr/bin/sac
  ln -rsv "${pkgdir}"/opt/sac/bin/sacinit.sh "${pkgdir}"/etc/profile.d/sacinit.sh
  ln -rsv "${pkgdir}"/opt/sac/bin/sacinit.csh "${pkgdir}"/etc/profile.d/sacinit.csh
}

# vim:set ts=2 sw=2 et:
