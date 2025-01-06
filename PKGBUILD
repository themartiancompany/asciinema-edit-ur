# SPDX-License-Identifier: AGPL-3.0
#
# Maintainer: Truocolo <truocolo@aol.com>
# Maintainer: Pellegrino Prevete (tallero) <pellegrinoprevete@gmail.com>
# Maintainer: Malachi Soord <me@malachisoord.com>

_git="false"
_pkg=asciinema-edit
pkgname="${_pkg}"
# pkgver=0.0.6.1
pkgver=0.0.6
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
  # _sum='106c8c4ac320a093cca59703e524817b12d206a6cc9e4d187c9d122a069855fc33c1410fe7119372373be5c614ab3bca9283d73f47b21da91cdffeff3a6d5fa2'
  _sum="SKIP"
fi
source=(
  "${_src}"
)
sha512sums=(
  "${_sum}"
)

prepare() {
  true
  # cp \
  #   -r \
  #   "${_tarname}/vendor" \
  #   "${srcdir}"
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
    mod \
      init \
      "${_pkg}"
  go \
    mod \
      tidy
  go \
    mod \
      vendor
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


