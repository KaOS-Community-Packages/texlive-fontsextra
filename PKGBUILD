pkgname=texlive-fontsextra
pkgver=2014.36711
_revnr=${pkgver#2014.}
pkgrel=1
pkgdesc="TeX Live - all sorts of extra fonts"
license=(GPL)
arch=('x86_64')
depends=('texlive-core')
groups=('texlive-most')
url='http://tug.org/texlive/'
source=("https://sources.archlinux.org/other/texlive/$pkgname-$pkgver-src.zip" "$pkgname.maps")
options=('!emptydirs')
install=texlive.install
md5sums=('389c020ccc722fef414248d7ebca202b'
         '18d5e8e0495329602b03c6734754ed71')

build() {
   cd "$srcdir"
   for p in *.tar.xz; do
	   bsdtar -xf $p
   done
   rm -rf {tlpkg,doc,source} || true
}

package() {
   cd "$srcdir"
   install -m755 -d $pkgdir/var/lib/texmf/arch/installedpkgs
   sed -i '/^#/d' CONTENTS
   install -m644 CONTENTS $pkgdir/var/lib/texmf/arch/installedpkgs/${pkgname}_${_revnr}.pkgs
   install -m644 $pkgname.maps $pkgdir/var/lib/texmf/arch/installedpkgs/
   install -m755 -d $pkgdir/usr/share
   wanteddirs=$(for d in *; do test -d $d && [[ $d != texmf* ]] && echo $d; done) || true
   for dir in $wanteddirs; do
     find $dir -type d -exec install -d -m755 $pkgdir/usr/share/texmf-dist/'{}' \;
     find $dir -type f -exec install -m644 '{}' $pkgdir/usr/share/texmf-dist/'{}' \;
   done
   if [[ -d texmf-dist ]]; then
     find texmf-dist -type d -exec install -d -m755 $pkgdir/usr/share/'{}' \;
     find texmf-dist -type f -exec install -m644 '{}' $pkgdir/usr/share/'{}' \;
   fi
   if [[ -d $pkgdir/usr/share/texmf-dist/scripts ]]; then
     find $pkgdir/usr/share/texmf-dist/scripts -type f -exec chmod a+x '{}' \;
   fi
}
