# Maintainer: Simon Perry <aur [at] sanxion [dot] net>
# Contributor: Bartlomiej Piotrowski <nospam@bpiotrowski.pl>
# Contributor: Jaroslav Lichtblau <dragonlord@aur.archlinux.org>
# Contributor: Jason Pierce <`echo 'moc tod liamg ta nosaj tod ecreip' | rev`>
# Contributor: Jeremy Cowgar <jeremy@cowgar.com>
# Contributor: Simon Perry <aur [at] sanxion [dot] net>
# Contributor: Christopher Larson <kergoth@gmail.com>

pkgname=dropbear
pkgver=2014.63
pkgrel=1
pkgdesc="Lightweight replacement for sshd"
arch=('i686' 'x86_64')
url="http://matt.ucc.asn.au/dropbear/dropbear.html"
license=('MIT')
depends=('zlib')
source=(http://matt.ucc.asn.au/$pkgname/releases/$pkgname-$pkgver.tar.bz2
        $pkgname-keygen.service
        $pkgname.service
        $pkgname@.service
        $pkgname.socket)
sha256sums=('595992de432ba586a0e7e191bbb1ad587727678bb3e345b018c395b8c55b57ae'
            'd3b1556fd4313ae588604d93c18623b7c26a0086d9a89b895ffc6f9c328fc268'
            'af217607ce6529a127fc07e8f27cb6412290271883a60b4cd152d7b504c6ecf9'
            'acf99d4bffd4ef715f27f1167d12efea77ca660ab32ae4065bc98c625a2fecc9'
            '3738145236d71b572c4e62f1b7e3a4480c4fa6c06a2ae283e8bc9e50cbd584c7')

build() {
  cd ${srcdir}/$pkgname-$pkgver

  sed -i 's|usr/libexec/sftp|usr/lib/ssh/sftp|' options.h

  ./configure --prefix=/usr
  LIBS="-lcrypt" make
}

package() {
  cd ${srcdir}/$pkgname-$pkgver

  DESTDIR=${pkgdir} make install

  # Configuration files
  install -d ${pkgdir}/etc/$pkgname
  install -D -m644 ${srcdir}/$pkgname-keygen.service ${pkgdir}/usr/lib/systemd/system/$pkgname-keygen.service
  install -D -m644 ${srcdir}/$pkgname.service ${pkgdir}/usr/lib/systemd/system/$pkgname.service
  install -D -m644 ${srcdir}/$pkgname@.service ${pkgdir}/usr/lib/systemd/system/$pkgname@.service
  install -D -m644 ${srcdir}/$pkgname.socket ${pkgdir}/usr/lib/systemd/system/$pkgname.socket

  # License file
  install -D -m644 LICENSE ${pkgdir}/usr/share/licenses/$pkgname/LICENSE
}
