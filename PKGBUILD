# Maintainer: TommyTran732 <contact@tommytran.io>
# Contributor: Frederic Bezies <fredbezies@gmail.com>, Cassandra Watergate (saltedcoffii) <cassandrajwatergate@gmail.com>, LSUtigers3131

pkgname=pamac-flatpak-gnome
pkgver=10.4.2
pkgrel=1
_pkgfixver=$pkgver

pkgdesc="A Gtk3 frontend for libalpm (with AUR, Flatpak, AppIndicator support, and GNOME integration)"
arch=('i686' 'x86_64' 'arm' 'armv6h' 'armv7h' 'aarch64')
url="https://gitlab.manjaro.org/applications/pamac"
license=('GPL3')
depends=('libnotify' 'libpamac-flatpak>=10.3.0' 'libhandy' 'git' 'fakeroot' 'pkgconf' 'polkit-gnome')
optdepends=('fwupd: support firmware updates')
makedepends=('gettext' 'itstool' 'vala>=0.45' 'meson' 'gobject-introspection' 'xorgproto' 'asciidoc')
conflicts=('pamac' 'pamac-cli' 'pamac-gtk' 'pamac-qt' 'pamac-classic' 'pamac-aur' 'pamac-aur-git' 'pamac-all' 'pamac-all-git' 'pamac-flatpak' 'pacmac-nosnap')
provides=('pamac')
options=(!emptydirs)
install=pamac.install
source=("pamac-$pkgver.tar.gz::$url/-/archive/v$pkgver/pamac-v$pkgver.tar.gz") 
sha512sums=('2e6a7106d154acff85e57e14066bb748e69c8e6831fb992790bfd2906f09defcb4bac399a6ddd33e369f4efe1c25f1367a19b8ffd71f69506d016adde9f6a805')

prepare() {
  # adjust version string
  sed -i -e "s|\"$_pkgfixver\"|\"$pkgver-$pkgrel\"|g" $srcdir/pamac-v$pkgver/src/version.vala
}

build() {
  arch-meson --buildtype=release -Denable-fake-gnome-software=true $srcdir/pamac-v$pkgver build
  meson compile -C build
}

check() {
  meson test -C build --print-errorlogs
}

package() {
  meson install -C build --destdir "$pkgdir"
}
