# SPDX-License-Identifier: AGPL-3.0
#
# Maintainer: Truocolo <truocolo@aol.com>
# Maintainer: Pellegrino Prevete (tallero) <pellegrinoprevete@gmail.com>
# Maintainer: Malachi Soord <me@malachisoord.com>

_git="false"
_pkg=asciinema-edit
pkgname="${_pkg}"
pkgver=0.0.6.1
_commit="28a7d761cd7cb112f23e43e2f2f948542cc0fc9f"
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
if [[ "${_git}" == "true" ]]; then
  makedepends+=(
    "git"
  )
  _src="${_tarname}::git+${url}#${_commit}"
  _sum="SKIP"
elif [[ "${_git}" == "false" ]]; then
  _src="${_tarname}.tar.gz::${url}/archive/refs/tags/${pkgver}.tar.gz"
  _sum='2c8af30b216bc168521bcc899c5e677ae40344e8a2b4ee19b8702f9517c50c1c787527bb4ea6157da8f43e053a56e3cd9d466f08e7e741a1f76247122cc4d654'
fi
source=(
  "${_src}"
)
sha512sums=(
  "${_sum}"
)

prepare() {
  cp \
    -r \
    "${_tarname}/vendor" \
    "${srcdir}"
}

build() {
  local \
    _go_opts=()
  _go_opts=(
    -tags
      "netgo"
    -v
    -a
    -ldflags
      "-X main.version=${pkgver} -extldflags \"-static\""
  )
  export CGO_CPPFLAGS="${CPPFLAGS}"
  export CGO_CFLAGS="${CFLAGS}"
  export CGO_CXXFLAGS="${CXXFLAGS}"
  export CGO_LDFLAGS="${LDFLAGS}"
  export GOFLAGS="-buildmode=pie -trimpath -ldflags=-linkmode=external -mod=readonly -modcacherw"
  cd \
    "${_tarname}"
  go \
    build \
      -o build \
      .
      # "${_go_opts[@]}" \
      # "main.go"
}

package() {
  install \
    -Dm755 \
    "${_pkg}" \
    "${pkgdir}/usr/bin/${_pkg}"
  install \
    -Dm644 \
    "LICENSE" \
    "${pkgdir}/usr/share/licenses/${pkgname}"
  install \
    -Dm644 \
    "README.md" \
    "${pkgdir}/usr/share/doc/${pkgname}/README.md"
}


