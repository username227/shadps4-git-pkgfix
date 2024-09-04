# Maintainer: Alexandre Bouvier <contact@amb.tf>
_pkgname=rpcsx
pkgname=$_pkgname-git
pkgver=r491.068d95c
pkgrel=1
pkgdesc="Sony PlayStation 4 emulator"
arch=('x86_64')
url="https://rpcsx.github.io/rpcsx-site/"
license=('GPL-2.0-only AND MIT')
depends=(
	'gcc-libs'
	'glfw>=3.3'
	'glibc'
	'libunwind'
	'spirv-tools'
	'python'
)
makedepends=(
	'cmake'
	'git'
	'glslang'
	'sox'
	'spirv-cross'
	'vulkan-headers>=1:1.3'	
	'vulkan-icd-loader>=1.3'
	'xbyak'
)
optdepends=('vulkan-validation-layers: for rpcsx-gpu --validate')
provides=("$_pkgname=${pkgver#r}")
conflicts=("$_pkgname")
source=("$_pkgname::git+https://github.com/RPCSX/rpcsx.git"
	"git+https://github.com/RPCSX/xbyak.git"
	"git+https://github.com/KhronosGroup/SPIRV-Tools.git"
	"git+https://github.com/KhronosGroup/SPIRV-Headers.git"
	"git+https://github.com/KhronosGroup/SPIRV-Cross.git"
	"git+https://github.com/KhronosGroup/glslang.git"
	"git+https://github.com/nlohmann/json.git"
	"modulesfix.patch")
b2sums=('SKIP'
        'SKIP'
        'SKIP'
        'SKIP'
        'SKIP'
        'SKIP'
        'SKIP'
        '77c0eca9b005e0624fd9c64454a3ecb9333e2ec1cde0302a946bd989f5a82bb30819d920f7f15bedacd44ecbdeaa01b83a22e0ee35b062d419fd72f1d7b01248')

pkgver() {
	cd $_pkgname
	printf "r%s.%s" "$(git rev-list --count HEAD)" "$(git rev-parse --short HEAD)"
}

prepare() {
	patch $srcdir/$_pkgname/.gitmodules modulesfix.patch
	cd $srcdir/$_pkgname
	git submodule init
    	for submodule in {xbyak,SPIRV-Tools,SPIRV-Headers,SPIRV-Cross,glslang,json};
    	do
    	git config submodule.${submodule}.url "$srcdir/${submodule}"
    	done
    	git -c protocol.file.allow=always submodule update
}

build() {
	cmake -S $_pkgname -B build \
		-DCMAKE_BUILD_TYPE=Release \
		-DCMAKE_CXX_FLAGS_RELEASE="-DNDEBUG" \
		-DCMAKE_INSTALL_PREFIX=/usr \
		-Wno-dev
	cmake --build build
}

package() {
	depends+=('libsox.so' 'libvulkan.so')
	# shellcheck disable=SC2154
	DESTDIR="$pkgdir" cmake --install build
	install -Dm644 -t "$pkgdir"/usr/share/licenses/$pkgname $_pkgname/orbis-kernel/LICENSE
}
