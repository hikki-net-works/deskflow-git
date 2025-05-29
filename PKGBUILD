_pkgname=deskflow
pkgname=$_pkgname-git
pkgver=v1.22.0.r109.g5d594dd
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
_commit=5d594dd6bebbe981925391fd5b15f5fb2258e298
source=("git+https://github.com/deskflow/deskflow.git#commit=$_commit")
sha256sums=('d25283521f02d4d527cc408798038aa4bd693d3dcf388b6e959d761ef4105126')
b2sums=('63bf30f8a9282235d27b491b0460202808e5aaca23d53ee5ef6fa86e74b4f8daf72ee750fdb327582f8f69d369f6e7c4dec20e62c217fd555681f6322087b312')

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
