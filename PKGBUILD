# Maintainer: thotypous <matiasΘarchlinux-br·org>

pkgname=eresi-svn
pkgver=1446
pkgrel=1
pkgdesc="Multi-architecture binary analysis framework based on a common domain-specific language for reverse engineering"
url="http://www.eresi-project.org"
arch=('i686' 'x86_64')
license=('GPL')
depends=('openssl' 'bash')
makedepends=('subversion')
provides=('eresi')
conflicts=('eresi')
source=()
md5sums=()

_svnmod="eresi"
_svntrunk="http://svn.eresi-project.org/svn/trunk/"

build() {
  cd "${srcdir}"

  msg "Getting sources..."
  svn co "${_svntrunk}" "${_svnmod}" -r "${pkgver}"
  cd "${_svnmod}"

  msg "Building..."

  _opts="--enable-32-64 --enable-readline --libasm-ia32 --libasm-sparc --libasm-mips --libasm-arm"
  [ "$CARCH" = "x86_64" ] && _opts="${_opts} --enable-m64"

  sed -i 's,/usr/local,/usr,g;s,ln -sf \\$([A-Z]\{3\}PATH),ln -sf ,;s,^GENTOO=.*$,GENTOO=1,' configure || return 1
  sed -i '/dprintf(/d' librevm/include/revm.h || return 1

  ./configure ${_opts} || return 1
  make || return 1
  make install DESTDIR="${pkgdir}" || return 1 

  rm -rf "${pkgdir}/usr/include/libelfsh/.svn"
}
