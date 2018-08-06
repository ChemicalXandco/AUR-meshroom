# Maintainer : bartus <arch-user-repoᘓbartus.33mail.com>

name=meshroom
#fragment="#commit=9bd70ed8ace83c6dde174178e17c5147bb50248f"
fragment="#branch=develop"
pkgname=${name}
pkgver=r783.80412d5
pkgrel=1
pkgdesc="Meshroom is a free, open-source 3D Reconstruction Software based on the AliceVision framework."
arch=('i686' 'x86_64')
url="http://alicevision.github.io/"
license=('MPL2')
groups=()
_depends_qt=(python-pyside2 qt5-quickcontrols{,2} qt5-3d qt5-graphicaleffects qt5-imageformats qt5-location qt5-svg)
#_depends_qt+=(qt5-datavis3d qt5-scxml)
depends=(alice-vision python python-psutil ${_depends_qt[@]})
makedepends=(git python-setuptools python-cx_freeze)
source=("${pkgname}::git+https://github.com/alicevision/meshroom.git${fragment}"
        "voctree::git+https://gitlab.com/alicevision/trainedVocabularyTreeData.git"
        )
md5sums=('SKIP'
         'SKIP')

pkgver() {
  cd "$pkgname"
  printf "r%s.%s" "$(git rev-list --count HEAD)" "$(git rev-parse --short HEAD)"
}

prepare() {
  cd ${srcdir}/${pkgname}
  msg2 "Hardcode camera_database and voctree default value"
  sed -i   "s:'ALICEVISION_VOCTREE', '':'ALICEVISION_VOCTREE', '/usr/share/${pkgname}/vlfeat_K80L3.SIFT.tree':g" meshroom/nodes/aliceVision/*.py
  sed -i "s:'ALICEVISION_SENSOR_DB', '':'ALICEVISION_SENSOR_DB', '/usr/share/aliceVision/sensor_width_camera_database.txt':g" meshroom/nodes/aliceVision/*.py
}

build() {
  cd ${srcdir}/${pkgname}
  python setup.py build
}


package() {
  cd ${srcdir}/${pkgname}
  python setup.py install --root=${pkgdir} --optimize=1 --skip-build
  install -Dm644 -t ${pkgdir}/usr/share/${pkgname} ${srcdir}/voctree/vlfeat_K80L3.SIFT.tree
}
# vim:set ts=2 sw=2 et:
