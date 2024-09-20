#!/bin/bash -e
#
# Maintainer: Ľubomír 'the-k' Kučera <lubomir.kucera.jr at gmail.com>
# Contributor: Jonian Guveli <https://github.com/jonian/>

_pkgname=gnome-shell-extension-clipboard-indicator
_uuid=clipboard-indicator@tudmotu.com
pkgname="${_pkgname}@the-k"
pkgver=71
pkgrel=1
pkgdesc="The most popular clipboard manager for GNOME"
arch=("any")
url="https://github.com/Tudmotu/gnome-shell-extension-clipboard-indicator"
license=("MIT")
provides=(
  "${_pkgname}"
)
conflicts=(
  "${_pkgname}"
  "gnome-shell-extension-clipboard-history"
)
source=("$_pkgname-$pkgver.tar.gz::$url/archive/v$pkgver.tar.gz")
sha256sums=('31d6c3694889b0f1c257b113926643e6a37610495f501cbd810eb2c14b9ebd85')

prepare() {
  cd "${_pkgname}-${pkgver}"

  sed -i \
    -e 's/\bREADME\.rst\b//' \
    -e 's/^\(install:\) all$/\1/' \
    Makefile
}

package() {
  depends=(
    "gnome-shell>=1:46"
    "gnome-shell<1:51"
  )

  : "${pkgdir:?}"

  cd "${_pkgname}-${pkgver}"

  make "INSTALLPATH=${pkgdir}/usr/share/gnome-shell/extensions/${_uuid}" install

  install -d "$pkgdir/usr/share/glib-2.0" \
    && mv "$pkgdir/usr/share/gnome-shell/extensions/$_uuid/schemas" "$_"
  rm -f "$pkgdir/usr/share/glib-2.0/schemas/gschemas.compiled"

  install -d "${pkgdir}/usr/share/licenses/${pkgname}" \
    && mv "${pkgdir}/usr/share/gnome-shell/extensions/${_uuid}/LICENSE.rst" "$_"
}

: "${arch[@]}"
: "${conflicts[@]}"
: "${depends[@]}"
: "${license[@]}"
: "${pkgdesc}"
: "${pkgrel}"
: "${provides[@]}"
: "${sha256sums[@]}"
: "${source[@]}"
