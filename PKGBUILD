# Maintainer: DMBuce <dmbuce@gmail.com>
pkgname=clicraft-devel-git
pkgver=0.0.7.19.gea7614a
pkgver() {
  cd "$srcdir/$_gitname"
  git describe --always | sed 's|-|.|g'
}
pkgrel=1
pkgdesc="A command-line wrapper for a minecraft or bukkit server."
arch=("any")
url="https://github.com/DMBuce/clicraft"
license=('BSD')
depends=("bash" "tmux" "curl" "java-runtime")
makedepends=("git" "asciidoc")
#checkdepends=()
optdepends=("c10t: for map.sh action script" "mcexplore: for explore.sh action script")
provides=('clicraft')
conflicts=('clicraft')
backup=("etc/clicraft/action.d/explore.sh"
        "etc/clicraft/action.d/map.sh"
        "etc/cron.d/clicraft"
        "etc/logrotate.d/clicraft")
install="$pkgname.install"
source=("$pkgname::git://github.com/DMBuce/clicraft.git#branch=devel"
        "$pkgname.install"
        "$pkgname.rc")
md5sums=('SKIP'
         '631669f302dffa059b4bdc915374d3d6'
         'dce883d9854859651b62b3477d0b5d4a')
_gitname="$pkgname"

build() {
  cd "$srcdir/$_gitname"

  autoconf
  ./configure --prefix=/usr \
              --libexecdir=/usr/lib \
              --sysconfdir=/etc \
              --localstatedir=/var \
              --with-mcexplore \
              --with-c10t
  make
}

package() {
  cd "$srcdir/$_gitname"
  make DESTDIR="$pkgdir" install

  install -Dm755 "$startdir/$pkgname.rc" "${pkgdir}/etc/rc.d/$pkgname"
  install -D -m 644 "$srcdir/$_gitname/LICENSE" "$pkgdir/usr/share/licenses/clicraft/LICENSE"
}

# vim:set ts=2 sw=2 et:
