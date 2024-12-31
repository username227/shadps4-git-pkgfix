# Maintainer: Alexandre Bouvier <contact@amb.tf>
_pkgname=shadps4
pkgname=$_pkgname-git
pkgver=0.5.0.r67.g48c51bd9
pkgrel=1
pkgdesc="Sony PlayStation 4 emulator"
arch=('aarch64' 'x86_64')
url="https://shadps4.net/"
license=('GPL-2.0-or-later')
depends=(
	'crypto++>=8.9'
	'gcc-libs'
	'glibc'
	'glslang>=14.2'
	'hicolor-icon-theme'
	'pugixml>=1.14'
	'sdl3>=1:3.1.3'
)
makedepends=(
	'boost>=1.84'
	'cmake>=3.16.3'
	'clang'
	'ninja'
	'ffmpeg'
	'fmt>=10.2'
	'git'
	'half>=1.12'
	'magic_enum>=0.9.6'
	'qt6-base'
	'qt6-multimedia'
	'qt6-tools'
	'rapidjson'
	'renderdoc'
	'robin-map>=1.3'
	'spirv-headers'
	'toml11>=4.2'
	'vulkan-headers>=1:1.3.289'
	'vulkan-memory-allocator>=3.1'
	'xbyak>=7.07'
	'xxhash>=0.8.2'
	'zlib'
	'zlib-ng>=2.1.7'
	'zycore-c' # 'zydis>=5'
)
optdepends=(
	'renderdoc: for graphics debugging'
	'vulkan-validation-layers: for vulkan debugging'
)
provides=("$_pkgname=$pkgver")
conflicts=("$_pkgname")
options=('!buildflags' '!debug')
source=(
	"$_pkgname::git+https://github.com/shadps4-emu/shadPS4.git"
	"$_pkgname-cryptopp::git+https://github.com/shadps4-emu/ext-cryptopp.git"
	"$_pkgname-cryptoppwiin::git+https://github.com/shadps4-emu/ext-cryptoppwin.git"
	"$_pkgname-zlib-ng::git+https://github.com/shadps4-emu/ext-zlib-ng.git"
	"$_pkgname-sdl3::git+https://github.com/shadps4-emu/ext-SDL.git"
	"$_pkgname-fmt::git+https://github.com/shadps4-emu/ext-fmt.git"
	"git+https://github.com/KhronosGroup/Vulkan-Headers.git"
	"git+https://github.com/GPUOpen-LibrariesAndSDKs/VulkanMemoryAllocator.git"
	"git+https://github.com/KhronosGroup/glslang.git"
	"git+https://github.com/Tessil/robin-map.git"
	"git+https://github.com/herumi/xbyak.git"
	"$_pkgname-winpthreads::git+https://github.com/shadps4-emu/winpthreads.git"
	"git+https://github.com/Neargye/magic_enum.git"
	"git+https://github.com/ToruNiina/toml11.git"
	"zydis::git+https://github.com/zyantific/zydis.git"
	"$_pkgname-sirit::git+https://github.com/shadps4-emu/sirit.git"
	"git+https://github.com/Cyan4973/xxHash.git"
	"$_pkgname-tracy::git+https://github.com/shadps4-emu/tracy.git"
	"$_pkgname-boost::git+https://github.com/shadps4-emu/ext-boost.git"
	"git+https://github.com/HowardHinnant/date.git"
	"$_pkgname-ffmpeg-core::git+https://github.com/shadps4-emu/ext-ffmpeg-core.git"
	"git+https://github.com/ROCm/half.git"
	"$_pkgname-imgui::git+https://github.com/shadps4-emu/ext-imgui.git"
	"git+https://github.com/zeux/pugixml.git"
	"$_pkgname-discord-rpc::git+https://github.com/shadps4-emu/ext-discord-rpc.git"
	"$_pkgname-libatrac9::git+https://github.com/shadps4-emu/ext-LibAtrac9.git"
	"libpng::git+https://github.com/pnggroup/libpng.git"
	"git+https://github.com/USCiLab/cereal"
	"git+https://github.com/KhronosGroup/MoltenVK"
	"git+https://github.com/KhronosGroup/SPIRV-Cross"
	"git+https://github.com/KhronosGroup/SPIRV-Headers"
	"git+https://github.com/doctest/doctest.git"
	"git+https://github.com/nlohmann/json.git"
	"git+https://github.com/alex-shpak/hugo-book.git"
	"git+https://github.com/zyantific/zycore-c"
)
b2sums=('SKIP'
        'SKIP'
        'SKIP'
        'SKIP'
        'SKIP'
        'SKIP'
        'SKIP'
        'SKIP'
        'SKIP'
        'SKIP'
        'SKIP'
        'SKIP'
        'SKIP'
        'SKIP'
        'SKIP'
        'SKIP'
        'SKIP'
        'SKIP'
        'SKIP'
        'SKIP'
        'SKIP'
        'SKIP'
        'SKIP'
        'SKIP'
        'SKIP'
        'SKIP'
        'SKIP'
        'SKIP'
        'SKIP'
        'SKIP'
        'SKIP'
        'SKIP'
        'SKIP'
        'SKIP'
        'SKIP')


pkgver() {
	cd $_pkgname
	git describe --long | sed 's/^v\.\?//;s/\([^-]*-g\)/r\1/;s/-/./g'
}

prepare() {
    cd "$srcdir/$_pkgname"
    git submodule init
    for submodule in {cryptopp-cmake,cryptopp,cryptoppwin,zlib-ng,sdl3,fmt,vulkan-headers,vma,glslang,robin-map,xbyak,winpthreads,magic_enum,toml11,zydis,sirit,xxhash,tracy,ext-boost,date,ffmpeg-core,half,dear_imgui,pugixml,discord-rpc,LibAtrac9,libpng,cereal,MoltenVK,SPIRV-Cross};
    do
    git config submodule.${submodule}.url "$srcdir/${submodule}"
    done
    git -c protocol.file.allow=always submodule update
    cd $srcdir/$_pkgname/externals/sirit
    git submodule init
    git config submodule.externals/sirit/externals/SPIRV-Headers.url ../SPIRV-Headers
    git -c protocol.file.allow-always submodule update
    cd $srcdir/$_pkgname/externals/toml11
    git submodule init
    for submodule in {doctest,json,hugo-book};
    do
    git config submodule.${submodule}.url "../{submodule}"
    done
    git -c protocol.file.allow=always submodule update
}

build() {
	cmake -B build -S $_pkgname -G Ninja \
		-DCMAKE_BUILD_TYPE=Release \
		-DCMAKE_C_FLAGS_RELEASE="-DNDEBUG" \
		-DCMAKE_CXX_COMPILER=clang++ \
		-DCMAKE_C_COMPILER=clang \
		-DCMAKE_CXX_FLAGS_RELEASE="-DNDEBUG" \
		-DCMAKE_INSTALL_PREFIX=/usr \
		-DCMAKE_SKIP_INSTALL_RPATH=ON \
		-DENABLE_QT_GUI=ON \
		-DENABLE_UPDATER=OFF \
		-DSIRIT_USE_SYSTEM_SPIRV_HEADERS=ON \
		-Wno-dev
	cmake --build build
}

package() {
	depends+=(
		'libavcodec.so'
		'libavformat.so'
		'libavutil.so'
		'libfmt.so'
		'libswresample.so'
		'libswscale.so'
		'libxxhash.so'
		'libz.so'
		# 'libZydis.so'
		'qt6-base'
		'qt6-multimedia'
	)
	# shellcheck disable=SC2154
	DESTDIR="$pkgdir" cmake --install build
}
