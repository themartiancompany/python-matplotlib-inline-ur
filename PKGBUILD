# SPDX-License-Identifier: AGPL-3.0

#    ----------------------------------------------------------------------
#    Copyright © 2025  Pellegrino Prevete
#
#    All rights reserved
#    ----------------------------------------------------------------------
#
#    This program is free software: you can redistribute it and/or modify
#    it under the terms of the GNU Affero General Public License as published by
#    the Free Software Foundation, either version 3 of the License, or
#    (at your option) any later version.
#
#    This program is distributed in the hope that it will be useful,
#    but WITHOUT ANY WARRANTY; without even the implied warranty of
#    MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
#    GNU Affero General Public License for more details.
#
#    You should have received a copy of the GNU Affero General Public License
#    along with this program.  If not, see <https://www.gnu.org/licenses/>.

# Maintainer: Truocolo <truocolo@aol.com>
# Maintainer: Truocolo <truocolo@0x6E5163fC4BFc1511Dbe06bB605cc14a3e462332b>
# Maintainer: Pellegrino Prevete (dvorak) <pellegrinoprevete@gmail.com>
# Maintainer: Pellegrino Prevete (dvorak) <dvorak@0x87003Bd6C074C713783df04f36517451fF34CBEf>
# Maintainer: Daniel M. Capella <polyzen@archlinux.org>
# Maintainer: Bruno Pagani <archange@archlinux.org>

_py="python"
_pyver="$( \
  "${_py}" \
    -V | \
    awk \
      '{print $2}')"
_pymajver="${_pyver%.*}"
_pyminver="${_pymajver#*.}"
_pynextver="${_pymajver%.*}.$(( \
  ${_pyminver} + 1))"
_pkg=matplotlib-inline
pkgname="${_py}-${_pkg}"
pkgver=0.1.7
pkgrel=2
pkgdesc='Inline Matplotlib backend for Jupyter'
arch=(
  'any'
)
_http="https://github.com"
_ns="ipython"
url="${_http}/${_ns}/${_pkg}"
license=(
  'BSD-3-Clause'
)
depends=(
  "${_py}-traitlets"
)
makedepends=(
  'git'
  "${_py}-build"
  "${_py}-installer"
  "${_py}-setuptools"
  "${_py}-wheel"
)
checkdepends=(
  'ipython'
  "${_py}-matplotlib"
)
optdepends=(
  "${_py}-matplotlib"
)
source=(
  "git+${url}.git#tag=${pkgver}"
)
b2sums=(
  '29a3742892040b2529234d7cd68f35b80ff240e83d7aee858a1447547e707dd405e32b887ec05e139eae1eba13a10a23e089a517659579c3f83eabc733f78d8a'
)

build() {
  cd \
    "${_pkg}"
  "${_py}" \
    -m \
      "build" \
    --wheel \
    --skip-dependency-check \
    --no-isolation
}

check() {
  cd \
    "${_pkg}"
  "${_py}" \
    -m \
      "venv" \
    --system-site-packages \
    "test-env"
  "test-env/bin/${_py}" \
    -m \
      "installer" \
      "dist/"*".whl"
  "test-env/bin/${_py}" \
    -c \
      'from matplotlib_inline.backend_inline import show'
}

package() {
  local \
    _site_packages
  _site_packages="$( \
    "${_py}" \
      -c \
        "import site; print(site.getsitepackages()[0])")"
  cd \
    "${_pkg}"
  "${_py}" \
    -m \
      "installer" \
    --destdir="${pkgdir}" \
    "dist/"*".whl"
  # Symlink license file
  install \
    -d \
    "${pkgdir}/usr/share/licenses/${pkgname}"
  ln \
    -s \
    "${_site_packages}/${_pkg//-/_}-${pkgver}.dist-info/LICENSE" \
    "${pkgdir}/usr/share/licenses/${pkgname}/LICENSE"
}

# vim:set ts=2 sw=2 et:
