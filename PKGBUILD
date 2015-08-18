#Contributor: karnath <karnathtorjian@gmail.com>
pkgname=zathura-girara-git
pkgver=20111211
pkgrel=3
pkgdesc="Vim like document viewer"
arch=('i686' 'x86_64')
url="https://pwmt.org/projects/zathura/"
license=('custom')
depends=('girara-gtk2-git')
makedepends=('git')
optdepends=('zathura-pdf-poppler: PDF support by using poppler'
'zathura-pdf-mupdf: PDF support by using mupdf'
'zathura-djvu: djvu support by using djvulibre'
'zathura-ps: PostSctipt support by using libspectre'
)
makedepends=('git')
install=zathura.install
conflicts=('zathura' 'zathura-git' 'zathura-girara-git')
provides=('zathura' 'zathura-git' 'zathura-girara-git')

_gitroot="git://pwmt.org/zathura.git"
_gitname="zathura"

build(){
  cd ${srcdir}
  msg "Connecting to GIT server..."

  if [ -d ${srcdir}/$_gitname ]; then
    cd $_gitname && git pull origin
    msg "The local files are updated."
  else
    git clone $_gitroot
    cd $_gitname && git checkout --track -b develop origin/develop
  fi

  msg "GIT checkout done or server timeout"
  msg "Starting make..."
 
  if [ -d ${srcdir}/$_gitname-build ]; then
    rm -rf ${srcdir}/$_gitname-build
  fi

  git clone ${srcdir}/$_gitname ${srcdir}/$_gitname-build || return 1
  cd ${srcdir}/$_gitname-build/ || return 1

  make DESTDIR="$pkgdir" install || return 1
  install -D -m664 zathurarc.5.rst "$pkgdir/usr/share/doc/$pkgname/zathurarc.5.rst"
  install -D -m664 LICENSE "$pkgdir/usr/share/licenses/$pkgname/LICENSE"
}

