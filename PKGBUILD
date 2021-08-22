# Maintainer: TommyTran732
# https://gitlab.manjaro.org/packages/extra/pamac

pkgname=pamac-flatpak-gnome
pkgver=10.1.3
pkgrel=3
_pkgfixver=$pkgver

pkgdesc="A Gtk3 frontend for libalpm (with AUR, Flatpak, AppIndicator support, and GNOME integration)"
arch=('i686' 'x86_64' 'arm' 'armv6h' 'armv7h' 'aarch64')
url="https://gitlab.manjaro.org/applications/pamac"
license=('GPL3')
depends=('libnotify' 'libpamac-flatpak' 'libhandy' 'libappindicator-gtk3' 'git' 'fakeroot' 'pkgconf')
makedepends=('gettext' 'itstool' 'vala>=0.45' 'meson' 'ninja' 'gobject-introspection' 'xorgproto' 'asciidoc')
conflicts=('pamac' 'pamac-cli' 'pamac-classic' 'pamac-aur' 'pamac-aur-git' 'pamac-all' 'pamac-all-git' 'pamac-flatpak' 'gnome-software' 'pamac-tray-appindicator')
provides=('pamac' 'gnome-software')
options=(!emptydirs)
install=pamac.install
source=("pamac-$pkgver.tar.gz::$url/-/archive/v$pkgver/pamac-v$pkgver.tar.gz") 
sha256sums=('577c0dfca155af9f4a7537b6c09bd37958ea5b5724c187f03239b27bd3d5951a')

prepare() {
  cd "$srcdir/pamac-v$pkgver"
  # adjust version string
  sed -i -e "s|\"$_pkgfixver\"|\"$pkgver-$pkgrel\"|g" src/version.vala
}

build() {
  cd "$srcdir/pamac-v$pkgver"
  mkdir -p builddir
  cd builddir
  meson --prefix=/usr --sysconfdir=/etc -Denable-flatpak=true -Denable-appindicator=true -Denable-fake-gnome-software=true --buildtype=release
  ninja
}

package() {
  cd "$srcdir/pamac-v$pkgver/builddir"
  DESTDIR="$pkgdir" ninja install
}