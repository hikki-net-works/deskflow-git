_pkgname=deskflow
pkgname=$_pkgname-git
pkgver=v1.23.0.r145.g34c439b
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
_commit=34c439b3de4518f770af09efd8f23a9b9df87fb6
source=("git+https://github.com/deskflow/deskflow.git#commit=$_commit")
sha256sums=('5fa00a2417f1eca272b2590ef133454b16d3044fc37c78d44f53fb7e1cb6cb8f')
b2sums=('1ba94575d8bbeba4886aff989609de9d73c4f608fd9d347fff1ac0a92ce5ea868e615422dfbd7022a5737291f7a52eab8e2d279043818576649f5a543c0f818a')

pkgver() {
  cd "$srcdir/$_pkgname"
  ( set -o pipefail
    git describe --long --abbrev=7 2>/dev/null | sed 's/\([^-]*-g\)/r\1/;s/-/./g' ||
    printf "r%s.%s" "$(git rev-list --count HEAD)" "$(git rev-parse --short=7 HEAD)"
  )
}

build() {
  cd "$srcdir/$_pkgname"
  
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
  cd "$srcdir/$_pkgname"
  export QT_QPA_PLATFORM=offscreen
  ./build/bin/legacytests
}

package() {
  cd "$srcdir/$_pkgname"
  DESTDIR="${pkgdir}" cmake --install build
  install -Dm 644 README.md doc/user/configuration.md -t "${pkgdir}/usr/share/doc/${_pkgname}"
}

# vim: ts=2 sw=2 et:
