# SPDX-License-Identifier: AGPL-3.0
#
# Maintainer: Truocolo <truocolo@aol.com>
# Maintainer: Pellegrino Prevete (tallero) <pellegrinoprevete@gmail.com>
# Maintainer: Malachi Soord <me@malachisoord.com>

_git="false"
_pkg=asciinema-edit
pkgname="${_pkg}"
pkgver=0.0.7.3
_commit="946ef32cd0cf8ffa39215c8c18c20793338b4102"
pkgrel=1
pkgdesc="asciinema casts post-production tools."
_http="https://github.com"
_ns="themartiancompany"
url="https://github.com/${_ns}/${_pkg}"
arch=(
  'x86_64'
  'arm'
  'aarch64'
  'armv7l'
  'armv6l'
  'mips'
  'pentium4'
  'powerpc'
)
makedepends=(
  'go'
)
license=(
  'AGPL3'
)
_tarname="${_pkg}-${pkgver}"
_tag_name="commit"
_tag="${_commit}"
if [[ "${_git}" == "true" ]]; then
  makedepends+=(
    "git"
  )
  _src="${_tarname}::git+${url}#${_tag_name}=${_tag}"
  _sum="SKIP"
elif [[ "${_git}" == "false" ]]; then
  _src="${_tarname}.tar.gz::${url}/archive/refs/tags/${pkgver}.tar.gz"
  _sum='ddf78ba6e2be27e5674364907a99f9dfa2b2519eeea53df340bf8a2fa73acb44e8fe849edc5280fd3d3c74f00b11488cf5c5de9d5c0fbd214b0e003a4e05f66f'
fi
source=(
  "${_src}"
)
sha512sums=(
  "${_sum}"
)

build() {
  local \
    _go_flags=()
  _go_flags=(
    -buildmode=pie
    -trimpath
    -ldflags=-linkmode=external
    -mod=vendor
    -modcacherw
  )
  export \
    CGO_CPPFLAGS="${CPPFLAGS}" \
    CGO_CFLAGS="${CFLAGS}" \
    CGO_CXXFLAGS="${CXXFLAGS}" \
    CGO_LDFLAGS="${LDFLAGS}" \
    GOFLAGS="${_go_flags[*]}"
  cd \
    "${_tarname}"
  go \
    build \
      -o \
        "${_pkg}" \
      "${_pkg}"
}

package() {
  cd \
    "${_tarname}"
  install \
    -Dm755 \
    "${_pkg}" \
    "${pkgdir}/usr/bin/${_pkg}"
  install \
    -Dm644 \
    "COPYING" \
    "${pkgdir}/usr/share/licenses/${pkgname}"
  install \
    -Dm644 \
    "LICENSE" \
    "${pkgdir}/usr/share/licenses/${pkgname}"
  install \
    -Dm644 \
    "README.md" \
    "${pkgdir}/usr/share/doc/${pkgname}/README.md"
}

