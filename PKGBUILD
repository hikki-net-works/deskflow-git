pkgname=deskflow
pkgver=1.21.0
pkgrel=1
pkgdesc='Share one mouse and keyboard between multiple computers'
url='https://deskflow.org/'
arch=(x86_64)
license=('GPL-2.0-only WITH LicenseRef-OpenSSL-Exception')
depends=(
  gcc-libs
  glib2
  glibc
  hicolor-icon-theme
  libei
  libglvnd
  libice
  libportal
  libsm
  libx11
  libxext
  libxi
  libxinerama
  libxkbcommon
  libxkbcommon-x11
  libxkbfile
  libxrandr
  libxtst
  openssl
  qt6-base
  tomlplusplus
)
makedepends=(
  cli11
  cmake
  git
  gtest
  ninja
  python
  qt6-tools
  xorgproto
)
source=("git+https://github.com/deskflow/deskflow.git#tag=v${pkgver}")
sha256sums=('53620ef0192bc92972a8e4ed8b633ad16ad0a8e220a07add97b6b756ac3d6d30')
b2sums=('89236004b08b1b5ac05a531d097da1acaafdc7f24330121967b36717e0f6aff22fe7c149d2effccf8e882afca1f88c20df1052afd8797faf7d39be88cc7edce5')

build() {
  cd "${pkgname}"
  cmake \
    -DCMAKE_INSTALL_PREFIX=/usr \
    -DCMAKE_BUILD_TYPE=None \
    -DCMAKE_C_FLAGS="${CFLAGS}" \
    -DCMAKE_CXX_FLAGS="${CXXFLAGS}" \
    -DCMAKE_EXE_LINKER_FLAGS="${LDFLAGS}" \
    -DCMAKE_SHARED_LINKER_FLAGS="${LDFLAGS}" \
    -Wno-dev \
    -G Ninja \
    -B build \
    -S .
  cmake --build build --verbose
}

check() {
  cd "${pkgname}"
  export QT_QPA_PLATFORM=offscreen
  ./build/bin/unittests
  ./build/bin/integtests
}

package() {
  cd "${pkgname}"
  DESTDIR="${pkgdir}" cmake --install build
  install -Dm 644 README.md doc/configuration.md -t "${pkgdir}/usr/share/doc/${pkgname}"
}

# vim: ts=2 sw=2 et:
