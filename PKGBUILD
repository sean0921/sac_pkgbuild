# Contributor: Sean Ho <sean.li.shin.ho@gmail.com>

pkgname=sac-iris
_pkgname=sac
pkgver=102.0
pkgrel=2
pkgdesc="The Seismic Analysis Code (SAC) is one of the most widely used analysis packages for regional and teleseismic seismic data."
arch=(x86_64)
url="http://ds.iris.edu/ds/nodes/dmc/forms/sac/"
license=('custom')
depends=('libx11' 'ncurses' 'readline')
source=("local://sac-${pkgver}.tar.gz")
sha256sums=('6815c2879d047f1f4961dbd52102ab131faac862661ec6a128ab00575b8abc12')

prepare() {
  cd "${srcdir}/${_pkgname}-${pkgver}"
  patch -p1 < ../../0001-refresh-DESTDIR-fix-patch.patch
  autoreconf -fiv
  ./configure --prefix /opt/sac/ --enable-readline
}

build() {
  cd "${srcdir}/${_pkgname}-${pkgver}"
  make || return 1
}

package() {
  mkdir -pv "${pkgdir}"/usr/bin/
  cd "${srcdir}/${_pkgname}-${pkgver}"
  make DESTDIR="${pkgdir}" install || return 1
  cp -v ../../sac_in_distro.sh "${pkgdir}"/usr/bin/sac
  chmod +x "${pkgdir}"/usr/bin/sac
}

# vim:set ts=2 sw=2 et:
