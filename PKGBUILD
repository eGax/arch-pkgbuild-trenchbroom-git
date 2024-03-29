# Maintainer: Hauke Rehfeld <aur@haukerehfeld.de>
# Contributor: Retro Gamer <https://github.com/eGax>

pkgname=trenchbroom-git
pkgver=v2024.1.RC2.r19.gce15d1158
pkgrel=1
pkgdesc="TrenchBroom is a free (GPLv3+), cross platform level editor for Quake-engine based games. It supports Quake, Quake 2, and Hexen 2.
This is the current commit build off of TrenchBroom's main GitHub branch. If you want the last official release use trenchbroom-bin."
arch=("i686" "x86_64")
url="https://trenchbroom.github.io/"
license=("GPL3")

makedepends=("git" "pandoc" "qt5-base" "cmake" "ninja" "qt5-svg" "libxcb" "zip" "unzip")
depends=("freeimage" "freetype2" "mesa" "libgl" "freeglut" "libxxf86vm" "glew" "glm" "tinyxml2")
conflicts=("trenchbroom")
provides=("trenchbroom")

source=("trenchbroom::git+https://github.com/TrenchBroom/TrenchBroom.git#branch=master"
	trenchbroom.desktop)

sha1sums=('SKIP'
          '028252ac86ec7f733e94589062eb316224887bd4')

pkgver() {
  cd "trenchbroom"
  git describe --long | sed 's/\([^-]*-g\)/r\1/;s/-/./g'
}

prepare() {
  cd trenchbroom
	# cmake requires a CmakeLists.txt from this submodule
	# -c submodule."lib/BinaryLibs".active=0
  git -c submodule."lib/freetype/freetype-windows-binaries".active=0 submodule update --init --recursive
}

_BUILDDIR=build

build() {
	mkdir -p "$_BUILDDIR"
	cd "$_BUILDDIR"
	cmake "$srcdir/trenchbroom" -DCMAKE_INSTALL_PREFIX:PATH=/usr -DCMAKE_BUILD_TYPE=Release -DCMAKE_PREFIX_PATH="cmake/packages" -DCMAKE_TOOLCHAIN_FILE="vcpkg/scripts/buildsystems/vcpkg.cmake"
	# we were running into weird xcb errors, which made this necessary to force headless builds
	# might be useful incase you ARE building on a headless system
	#QT_QPA_PLATFORM=offscreen cmake --build . --target TrenchBroom
	cmake --build . --target TrenchBroom
}

package() {
	install -Dm644 trenchbroom.desktop "${pkgdir}/usr/share/applications/trenchbroom.desktop"
	cd "${srcdir}/$_BUILDDIR"
	make DESTDIR="${pkgdir}" install
	install -Dm644 "${srcdir}/trenchbroom/app/resources/linux/icons/icon_256.png" "${pkgdir}/usr/share/pixmaps/trenchbroom.png"
}
