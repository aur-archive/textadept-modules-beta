# Maintainer: Niklas Wallén <nikw at gmx dot com>

pkgname=textadept-modules-beta
_version=8.0
pkgver=8.0
pkgrel=1
pkgdesc="Official modules for Textadept"
arch=('i686' 'x86_64')
url="http://foicica.com/textadept"
license=('MIT')
depends=('python')
provides=("textadept-modules=$pkgver")
conflicts=('textadept-modules')
source=("http://foicica.com/textadept/download/textadept_${_version}.modules.zip"
        "LICENSE")
md5sums=('fe998fdd3627ee2565edd3abc11855a9'
         '91399f166258afd22907d1f7c3be2925')

package() {
  cd "$srcdir/textadept_${_version}.modules/modules"

  (cd yaml/src; make)

  for _mod in css html python rest ruby; do
    install -d "$pkgdir/opt/textadept/modules/$_mod"
    install -m644 "$_mod/"* "$pkgdir/opt/textadept/modules/$_mod/"
  done

  # modules containing shared libraries
  for _mod in yaml; do
    install -d "$pkgdir/opt/textadept/modules/$_mod"
    install -m644 "$_mod/"*.lua "$pkgdir/opt/textadept/modules/$_mod/"
    install -d "$pkgdir/opt/textadept/modules/$_mod"
    if [ "$CARCH" == "i686" ]; then
      install -m644 $_mod/*[^64][^osx].so "$pkgdir/opt/textadept/modules/$_mod/"
    else
      install -m644 $_mod/*64.so "$pkgdir/opt/textadept/modules/$_mod/"
	fi
  done

  install -d "$pkgdir/usr/share/licenses/$pkgname"
  install -m644 "$srcdir/LICENSE" \
      "$srcdir/textadept_${_version}.modules/modules/yaml/src/LICENSE"* \
	  "$pkgdir/usr/share/licenses/$pkgname/"
}
