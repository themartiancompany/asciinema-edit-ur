# SPDX-License-Identifier: AGPL-3.0
#
# Maintainer: Truocolo <truocolo@aol.com>
# Maintainer: Pellegrino Prevete (tallero) <pellegrinoprevete@gmail.com>
# Maintainer: Malachi Soord <me@malachisoord.com>

_os="$( \
  uname \
    -o)"
_git="false"
_pkg=asciinema-edit
pkgname="${_pkg}"
pkgver=0.0.7.4
_commit="498a776768222aa5fb534fab9721a69a2def590a"
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
if [[ "${_os}" == "Android" ]]; then
  _go="golang"
elif [[ "${_os}" == "GNU/Linux" ]]; then
  _go="go"
fi
makedepends=(
  "${_go}"
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
  _sum='421c9dd1f751d592946047956c9f3ebe2fe656439152a0a8c5eecc2b11ace4f1a76fa64dc90431c6c0a0251ec3a11a9cd57e4305d17d4f078974439189001486'
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

