_pkgname=deskflow
pkgname=$_pkgname-git
pkgver=v1.23.0.r0.g56f7a0d
pkgrel=1
pkgdesc='Share one mouse and keyboard between multiple computers'
url='https://deskflow.org/'
arch=(x86_64 x86_64_v3 aarch64)
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
  qt6-svg
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
_commit=56f7a0d7b5095ca1f1fa9a3e663cc30d40e3bc54
source=("git+https://github.com/deskflow/deskflow.git#commit=$_commit")
sha256sums=('25dd0db9ba3b7ef7b3080ceafd08317d2138ae29461ee462aa5be9bd2f16b67e')
b2sums=('941a0959005260ea156d4356368c04c46c15ce4cdc88c754a52a15d41ee13b45ac26dc8f5e93c3ae3c4c1c37cda6cd8460ddc28885b73a4bf9c0677e91ef0cc2')

pkgver() {
  cd "$_pkgname"
  ( set -o pipefail
    git describe --long --abbrev=7 2>/dev/null | sed 's/\([^-]*-g\)/r\1/;s/-/./g' ||
    printf "r%s.%s" "$(git rev-list --count HEAD)" "$(git rev-parse --short=7 HEAD)"
  )
}

build() {
  cd "${_pkgname}"
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
  cd "${_pkgname}"
  export QT_QPA_PLATFORM=offscreen
  ./build/bin/legacytests
}

package() {
  cd "${_pkgname}"
  DESTDIR="${pkgdir}" cmake --install build
  install -Dm 644 README.md doc/user/configuration.md -t "${pkgdir}/usr/share/doc/${_pkgname}"
}

# vim: ts=2 sw=2 et:
