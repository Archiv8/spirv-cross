#!/bin/bash

# Disable various shellcheck rules that produce false positives in this file.
# Repository rules should be added to the .shellcheckrc file located in the
# repository root directory, see https://github.com/koalaman/shellcheck/wiki
# and https://archiv8.github.io for further information.
# shellcheck disable=SC2034,SC2154
# [ToDo]: Add files: User documentation
# [ToDo]: Add files: Tooling
# [FixMe]: Namcap warnings and errors

# Maintainer: Ross Clark <https://github.com/Archiv8/spirv-cross/discussions>
# Contributor: Ross Clark <https://github.com/Archiv8/spirv-cross/discussions>

_relname="SPIRV-Cross"

pkgname="spirv-cross"
pkgver=1.3.216.0
pkgrel=1
pkgdesc="A tool and library for parsing and converting SPIR-V to other shader languages"
arch=(
  "x86_64"
  )
url="https://github.com/KhronosGroup/SPIRV-Cross/"
license=(
  "Apache"
  )
depends=(
  "sh"
  "gcc-libs"
  "spirv-headers"
  "spirv-tools"
  )
makedepends=(
  "git" 
  "cmake" 
  "python" 
  "python-nose")
_tarname="${_relname}-sdk-${pkgver}"
source=(
  "${_tarname}.tar.gz"::"https://github.com/KhronosGroup/${_relname}/archive/refs/tags/sdk-${pkgver}.tar.gz"
)
sha512sums=(
  "746bc4560c02d2658b4b9c2ed589e028fcd5708030a751343906076825bda0ae6547aa54c3f0128bbc00198c0c2d5dbc22409eeb0e99bf623696e2771c0cf158"
)

# prepare() {
#     mkdir -p SPIRV-Cross/external/{glslang,spirv-tools}

#    ln -sf "${srcdir}/glslang"       SPIRV-Cross/external/glslang
#     ln -sf "${srcdir}/SPIRV-Tools"   SPIRV-Cross/external/spirv-tools
#     ln -sf "${srcdir}/SPIRV-Headers" SPIRV-Tools/external/spirv-headers
# }

build() {
    # NOTE: test suite fails when using "None" build type
    local -a _common_opts=("-DCMAKE_BUILD_TYPE:STRING=Release" "-Wno-dev")

    cmake -B build-SPIRV-Cross -S ${_tarname} \
        "${_common_opts[@]}" \
        -DCMAKE_INSTALL_PREFIX:PATH="/usr" \
        -DSPIRV_CROSS_FORCE_PIC:BOOL="ON" \
        -DSPIRV_CROSS_SHARED:BOOL="ON"

    make -C build-SPIRV-Cross
}

check() {

    make -C build-SPIRV-Cross test
}

package() {

    make -C build-SPIRV-Cross DESTDIR="$pkgdir" install
}
