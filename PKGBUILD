# Maintainer: SelfRef <arch@selfref.dev>

# INFO: This version only supports X11 and uses old name. Use git or beta version for Wayland.

_basename=deskflow
pkgname=${_basename}
pkgver=1.17.0.r1
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
sha256sums=('39928f513169fef741b98c756e52c703072959a0d8aa03ab15d91d6f03ca5391')

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
