# Maintainer: Edward Davis <idlyby@proton.me>
# Contributor: ThatOneCalculator <kainoa@t1c.dev>
# Based on the xdg-desktop-portal-wlr-git PKGBUILD

_pkgname="xdg-desktop-portal-hyprland"
pkgname="${_pkgname}-git"
pkgver=1.3.6.r1.gfb9c8d66
pkgrel=2
pkgdesc="xdg-desktop-portal backend for hyprland"
url="https://github.com/hyprwm/xdg-desktop-portal-hyprland"
arch=(x86_64)
license=(BSD-3-Clause)
provides=("${pkgname%-git}" "xdg-desktop-portal-impl")
conflicts=("${pkgname%-git}")
depends=("libpipewire" "libinih" "qt6-base" "qt6-wayland" "wayland" "sdbus-cpp-git" "libdrm" "xdg-desktop-portal" "mesa" "hyprlang-git" "hyprwayland-scanner-git>=0.4.2" "hyprutils-git")
makedepends=("git" "wayland-protocols" "scdoc" "cmake" "hyprland-protocols-git")
optdepends=(
  "grim: required for the screenshot portal to function"
  "slurp: support for interactive mode for the screenshot portal; one of the built-in chooser options for the screencast portal"
  "hyprland: the Hyprland compositor"
)
source=("${_pkgname}::git+$url.git")
sha256sums=('SKIP')

backup=("usr/share/xdg-desktop-portal/hyprland-portals.conf")

pkgver() {
	cd "${_pkgname}"
    git describe --long --tags --abbrev=8 --exclude='*[a-zA-Z][a-zA-Z]*' \
	  | sed -E 's/^[^0-9]*//;s/([^-]*-g)/r\1/;s/-/./g'
}

prepare() {
	cd "${srcdir}/${_pkgname}"
	git submodule update --init
}

build() {
	cd "${srcdir}/${_pkgname}"

	cmake -DCMAKE_INSTALL_LIBEXECDIR=/usr/lib -DCMAKE_BUILD_TYPE=Release -DCMAKE_INSTALL_PREFIX=/usr -S . -B build -Wno-dev
	cmake --build build --config Release --target all
}

package() {
	cd "${srcdir}/${_pkgname}"

	DESTDIR="${pkgdir}" cmake --install build

	install -Dm644 LICENSE -t "${pkgdir}/usr/share/licenses/${_pkgname}"
}
