
pkgname=curl
pkgver=7.52.1
pkgrel=1
pkgdesc="An URL retrival utility and library"
arch=('x86_64')
url="https://curl.haxx.se"
license=('MIT')
depends=('zlib' 'openssl' 'bash' 'ca-certificates' 'libssh2' 'libpsl') # 'libidn' https://curl.haxx.se/mail/lib-2016-11/0033.html)
provides=('curl')
conflicts=('curl')
options=('!libtool')
source=("https://curl.haxx.se/download/${pkgname}-${pkgver}.tar.bz2"
        'curlbuild.h')
md5sums=('dd014df06ff1d12e173de86873f9f77a'
         '751bd433ede935c8fae727377625a8ae')

build() {
    cd ${pkgname}-${pkgver}

    ./configure \
        --with-random=/dev/urandom \
        --prefix=/usr \
        --mandir=/usr/share/man \
        --enable-ipv6 \
        --disable-ldaps \
        --disable-ldap \
        --enable-manual \
        --disable-versioned-symbols \
        --enable-threaded-resolver \
        --with-ca-bundle=/etc/ssl/certs/ca-certificates.crt \
        --without-libidn \
        --enable-threaded-resolver
    make
}

package() {
    cd ${pkgname}-${pkgver}
    make DESTDIR=${pkgdir} install
    
    install -Dm644 COPYING ${pkgdir}/usr/share/licenses/${pkgname}/COPYING
    install -Dm644 docs/libcurl/libcurl.m4 ${pkgdir}/usr/share/aclocal/libcurl.m4
    
    mv ${pkgdir}/usr/include/curl/curlbuild.h ${pkgdir}/usr/include/curl/curlbuild-64.h
    install -m 644 ${srcdir}/curlbuild.h ${pkgdir}/usr/include/curl/curlbuild.h
}
