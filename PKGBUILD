# $Id: PKGBUILD 129559 2015-03-19 07:36:14Z tpowa $
# Maintainer: Ray Rashif <schiv@archlinux.org>
# Contributor: Mateusz Herych <heniekk@gmail.com>
# Contributor: Charles Lindsay <charles@chaoslizard.org>

pkgname=vhba-module-lts
_srcname=vhba-module
pkgver=20140928
_extramodules=extramodules-3.14-lts
pkgrel=10
pkgdesc="Kernel module that emulates SCSI devices"
arch=('i686' 'x86_64')
url="http://cdemu.sourceforge.net/"
license=('GPL')
depends=('linux-lts>=3.14' 'linux-lts<3.20')
makedepends=('linux-lts-headers>=3.14' 'linux-lts-headers<3.20')
options=(!makeflags)
provides=('vhba-module')
install=$pkgname.install
source=("http://downloads.sourceforge.net/cdemu/$_srcname-$pkgver.tar.bz2"
        '60-vhba.rules')
md5sums=('967007230bb028424216d9b35da422c0'
         '4dc37dc348b5a2c83585829bde790dcc')

prepare() {
  cd $_srcname-$pkgver
}

build() {
  cd $_srcname-$pkgver
  _kernver="$(cat /usr/lib/modules/$_extramodules/version)"
  make KDIR=/usr/lib/modules/$_kernver/build
}

package() {
  cd $_srcname-$pkgver
  install -Dm644 vhba.ko "$pkgdir/usr/lib/modules/$_extramodules/vhba.ko"
  install -Dm644 ../60-vhba.rules "$pkgdir/usr/lib/udev/rules.d/60-vhba.rules"

  cd $startdir
  cp -f $install ${install}.pkg
  true && install=${install}.pkg
  sed -i "s/EXTRAMODULES=.*/EXTRAMODULES=$_extramodules/" $install
}

# vim:set ts=2 sw=2 et:
