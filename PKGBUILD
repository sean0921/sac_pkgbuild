# Contributor: Sean Ho <sean.li.shin.ho@gmail.com>

pkgname=sac-iris
_pkgname=sac
pkgver=101.6a
pkgrel=1
pkgdesc="The Seismic Analysis Code (SAC) is one of the most widely used analysis packages for regional and teleseismic seismic data."
arch=(x86_64)
url="http://ds.iris.edu/ds/nodes/dmc/forms/sac/"
license=('custom')
depends=('libx11' 'ncurses' 'readline')
source=("local://sac-${pkgver}-source.tar.gz")
md5sums=('627d8b239dd6b70dad8a7bfd6e5e7c7f')

prepare() {
  cd "${srcdir}/${_pkgname}-${pkgver}"
  patch -p1 < ../../0001-Fix-missing-DESTDIR-variable-in-Makefile.patch
  rm -vf bin/sac-config bin/sacinit.csh bin/sacinit.sh
  cd "${srcdir}/${_pkgname}-${pkgver}"
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
