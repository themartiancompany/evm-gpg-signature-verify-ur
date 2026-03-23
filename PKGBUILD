# SPDX-License-Identifier: AGPL-3.0

#    ----------------------------------------------------------------------
#    Copyright © 2024, 2025, 2026  Pellegrino Prevete
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

# Maintainers:
#   Truocolo
#     <truocolo@aol.com>
#     <truocolo@0x6E5163fC4BFc1511Dbe06bB605cc14a3e462332b>
#   Pellegrino Prevete (dvorak)
#     <pellegrinoprevete@gmail.com>
#     <dvorak@0x87003Bd6C074C713783df04f36517451fF34CBEf>

_evmfs_available="$(
  command \
    -v \
    "evmfs" || \
    true)"
if [[ ! -v "_evmfs" ]]; then
  if [[ "${_evmfs_available}" != "" ]]; then
    _evmfs="true"
  elif [[ "${_evmfs_available}" == "" ]]; then
    _evmfs="false"
  fi
fi
_os="$(
  uname \
    -o)"
if [[ ! -v "_offline" ]]; then
  _offline="false"
fi
if [[ ! -v "_git" ]]; then
  _git="false"
fi
if [[ ! -v "_git_service" ]]; then
  _git_service="github"
fi
if [[ ! -v "_ns" ]]; then
  _ns="themartiancompany"
fi
if [[ ! -v "_docs" ]]; then
  _docs="true"
fi
if [[ ! -v "_tag_name" ]]; then
  _tag_name="commit"
fi
if [[ ! -v "_archive_format" ]]; then
  if [[ "${_git}" == "false" ]]; then
    if [[ "${_git_service}" == "github" ]]; then
      if [[ "${_tag_name}" == "commit" ]]; then
        _archive_format="zip"
      elif [[ "${_tag_name}" == "pkgver" ]]; then
        _archive_format="tar.gz"
      fi
    fi
  fi
fi
_py="python"
pkgbase=evm-gpg-signature-verify
pkgname=(
  "${pkgbase}"
)
if [[ "${_docs}" == "true" ]]; then
  pkgname+=(
    "${pkgbase}-docs"
  )
fi
pkgver="0.0.0.0.0.0.0.0.0.0.0.1"
_commit="f3119e390abca7bc4bc313c3d351f31b7799cb24"
pkgrel=4
_pkgdesc=(
  "Checks if a file is cryptographically signed"
  "by an Ethereum Virtual Machine-compatible blockchain"
  "network user using one of its"
  "EVM OpenPGP Key Server self-published keys."
)
pkgdesc="${_pkgdesc[*]}"
arch=(
  'any'
)
_http="https://${_git_service}.com"
url="${_http}/${_ns}/${pkgname}"
license=(
  'AGPL3'
)
depends=(
  'evm-openpgp-keyserver'
  "findutils"
  'gpg-signature-info'
  'gpg-signature-verify'
  "libcrash-bash"
)
if [[ "${_os}" != "GNU/Linux" ]] && \
   [[ "${_os}" == "Android" ]]; then
  depends+=(
  )
fi
optdepends=(
)
[[ "${_os}" == 'Android' ]] && \
  optdepends+=(
  )
makedepends=(
  'make'
)
if [[ "${_docs}" == "true" ]]; then
  makedepends+=(
    "${_py}-docutils"
  )
fi
if [[ "${_git}" == "true" ]]; then
  makedepends+=(
    "git"
  )
fi
if [[ "${_evmfs}" == "true" ]]; then
  makedepends+=(
    "evmfs"
  )
fi
checkdepends=(
  "shellcheck"
)
source=()
sha256sums=()
_url="${url}"
if [[ ! -v "_tag" ]]; then
  if [[ "${_tag_name}" == "commit" ]]; then
    _tag="${_commit}"
  elif [[ "${_tag_name}" == "pkgver" ]]; then
    _tag="${pkgver}"
  fi
fi
_tarname="${pkgname}-${_tag}"
_tarfile="${_tarname}.${_archive_format}"
if [[ "${_offline}" == "true" ]]; then
  _url="file://${HOME}/${pkgname}"
fi
_github_release_sum="SKIP"
_github_release_sig_sum="SKIP"
_github_sum="94e85426d9053f3aae3116ea627816188f02752e5fec0ac391338b70a8a4c0c0"
_github_sig_sum="53c77cf4b3ba41802e1331b9505ef0b12262f0ab9c649545f9119786ed917df4"
_archive_sum="${_github_sum}"
_archive_sig_sum="${_github_sig_sum}"
# Dvorak
_evmfs_ns="0x87003Bd6C074C713783df04f36517451fF34CBEf"
_evmfs_network="100"
_evmfs_address="0x69470b18f8b8b5f92b48f6199dcb147b4be96571"
_evmfs_dir="evmfs://${_evmfs_network}/${_evmfs_address}/${_evmfs_ns}"
_evmfs_archive_uri="${_evmfs_dir}/${_archive_sum}"
_evmfs_archive_src="${_tarfile}::${_evmfs_archive_uri}"
_archive_sig_uri="${_evmfs_dir}/${_archive_sig_sum}"
_archive_sig_src="${_tarfile}.sig::${_archive_sig_uri}"
if [[ "${_evmfs}" == "true" ]]; then
  if [[ "${_git}" == false ]]; then
    _src="${_evmfs_archive_src}"
    _sum="${_archive_sum}"
    source+=(
      "${_archive_sig_src}"
    )
    sha256sums+=(
      "${_archive_sig_sum}"
    )
  elif [[ "${_git}" == "true" ]]; then
    _msg=(
      "Program git repository not uploaded"
      "on the EVMFS."
    )
    echo \
      "${_msg[*]}"
    return \
      1
  fi
elif [[ "${_evmfs}" == "false" ]]; then
  if [[ "${_git}" == "true" ]]; then
    _src="${_tarname}::git+${_url}#${_tag_name}=${_tag}?signed"
    _sum="SKIP"
  elif [[ "${_git}" == false ]]; then
    if [[ "${_tag_name}" == 'pkgver' ]]; then
      _src="${_tarfile}::${_url}/archive/refs/tags/${_tag}.${_archive_format}"
      _sum="${_github_release_sum}"
    elif [[ "${_tag_name}" == "commit" ]]; then
      _src="${_tarfile}::${_url}/archive/${_commit}.${_archive_format}"
      _sum="${_archive_sum}"
    fi
  fi
fi
source+=(
  "${_src}"
)
sha256sums+=(
  "${_sum}"
)
validpgpkeys=(
  # Truocolo <truocolo@aol.com>
  '97E989E6CF1D2C7F7A41FF9F95684DBE23D6A3E9'
  # Truocolo <truocolo@0x6E5163fC4BFc1511Dbe06bB605cc14a3e462332b>
  'F690CBC17BD1F53557290AF51FC17D540D0ADEED'
  # Pellegrino Prevete (dvorak) <dvorak@0x87003Bd6C074C713783df04f36517451fF34CBEf>
  '12D8E3D7888F741E89F86EE0FEC8567A644F1D16'
)

check() {
  cd \
    "${_tarname}"
  make \
    -k \
    check
}

package_evm-gpg-signature-verify() {
  cd \
    "${_tarname}"
  make \
    PREFIX="/usr" \
    DESTDIR="${pkgdir}" \
    install-scripts
  install \
    -Dm644 \
    "COPYING" \
    -t \
    "${pkgdir}/usr/share/licenses/${pkgname}/"
}

package_evm-gpg-signature-verify-docs() {
  cd \
    "${_tarname}"
  make \
    PREFIX="/usr" \
    DESTDIR="${pkgdir}" \
    install-doc
  make \
    PREFIX="/usr" \
    DESTDIR="${pkgdir}" \
    install-man
  install \
    -Dm644 \
    "COPYING" \
    -t \
    "${pkgdir}/usr/share/licenses/${pkgbase}-docs/"
}

# vim: ft=sh syn=sh et
