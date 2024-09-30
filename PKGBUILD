# Maintainer: SelfRef <arch@selfref.dev>

# INFO: This version only supports X11 and uses old name. Use git or beta version for Wayland.

_basename=deskflow
pkgname=${_basename}
pkgver=1.15.1.r1
pkgrel=1
pkgdesc="Deskflow lets you share one mouse and keyboard between multiple computers (stable version)"
arch=('x86_64')
url="https://deskflow.org/"
license=('GPL-2.0')
depends=(
	'libxtst'
	'libxkbcommon'
	'libnotify'
	# 'libei' # not yet used in this version
	# 'libportal' # not yet used in this version
	'qt6-base'
	'gdk-pixbuf2'
	'pugixml'
	'libxkbcommon-x11' # make optional for next version
	'libxinerama' # make optional for next version
	'libxrandr' # make optional for next version
	# 'libx11: X11 support' # dependency of libxtst
	# 'libxext: X11 support' # dependency of libxtst
	# 'libxi: X11 support' # dependency of libxtst
)
makedepends=(
	'git'
	'cmake'
	'libxkbfile'
	'gtest'
	'tomlplusplus'
	'cli11'
)
optdepends=(
	'openssl: TLS encryption'
	'gtk3: GTK file/dir picker'
)
provides=("$_basename")
conflicts=("$_basename" 'synergy')
source=("$_basename::git+https://github.com/deskflow/deskflow.git#tag=${pkgver/.r/+r}")
sha256sums=('0067a3c6e23fc3adc7a7e5a7af0520885a4a0193c13c031f4e123683fa9b480d')

prepare() {
	cd "$_basename"
	cmake -B build
}

build() {
	cd "$_basename"
	cmake --build build
}

check() {
	cd "$_basename"
	./build/bin/unittests
	./build/bin/integtests
}

package() {
	cd "$_basename"
	DESTDIR="$pkgdir" cmake --install build
}
