# Maintainer: Miroslav Koskar (http://miroslavkoskar.com/)

# Based on bitlbee-3.2.2-1:
# * Contributor: FUBAR <mrfubar@gmail.com>
# * Contributor: simo <simo@archlinux.org>
# * Contributor: Jeff 'codemac' Mickey <jeff@archlinux.org>
# * Contributor: Daniel J Griffiths <ghost1227@archlinux.us>
# * Contributor: Gaetan Bisson <bisson@archlinux.org>
# * Maintainer: Dave Reisner <dreisner@archlinux.org>

pkgname=bitlbee-skype-displayname-patch
pkgname_=bitlbee
pkgver=3.2.2
pkgrel=2
pkgdesc='BitlBee with skype protocol patch to properly handle full/display names'
url='http://github.com/mkoskar/pkgbuilds/tree/master/bitlbee-skype-displayname-patch'
license=('GPL')
arch=('i686' 'x86_64')
provides=('bitlbee')
conflicts=('bitlbee')
depends=('gnutls' 'glib2' 'libevent')
makedepends=('asciidoc' 'libotr')
optdepends=('skype4py: to use skyped'
            'libotr: for OTR encryption support')
source=("http://get.bitlbee.org/src/$pkgname_-$pkgver.tar.gz"
        'bitlbee.tmpfiles'
        'skype-displayname.patch')
sha1sums=('7e3cfe2b6bf4e8e603c74e7587307a6f5d267e9c'
          '3695ed2fe22436c4d0fc3ead829f7d1f89bc491c'
          '3e04d73ca9b045a465d761383d30ec1c49259e80')
backup=('etc/bitlbee/bitlbee.conf'
        'etc/bitlbee/motd.txt')
install=bitlbee.install

build() {
  cd "$pkgname_-$pkgver"

  patch -p0 <../skype-displayname.patch

  ./configure \
    --prefix=/usr \
    --etcdir=/etc/bitlbee \
    --sbindir=/usr/bin \
    --pidfile=/run/bitlbee/bitlbee.pid \
    --ipcsocket=/run/bitlbee/bitlbee.sock \
    --systemdsystemunitdir=/usr/lib/systemd/system \
    --ssl=gnutls \
    --events=libevent \
    --strip=0 \
    --otr=plugin \
    --skype=plugin

  make
}

package() {
  make -C "$pkgname_-$pkgver" DESTDIR="$pkgdir" install{,-etc,-dev,-systemd}

  install -o65 -g65 -dm770 "$pkgdir/var/lib/bitlbee"
  install -Dm644 "$srcdir/bitlbee.tmpfiles" "$pkgdir/usr/lib/tmpfiles.d/bitlbee.conf"
}
