pkgname=curl-kcp
_pkgname=curl
pkgver=8.5.0
pkgrel=1
pkgdesc="An URL retrival utility and library"
arch=('x86_64')
url="https://curl.haxx.se"
license=('MIT')
depends=('zlib' 'openssl' 'bash' 'ca-certificates' 'libssh2' 'libpsl')
conflicts=('libcurl-compat')
provides=('libcurl-compat')
options=('!libtool')
source=("https://curl.haxx.se/download/${_pkgname}-${pkgver}.tar.bz2")
md5sums=('d617745a3fd4456b591da53052a5ea94')

build() {
    cd ${_pkgname}-${pkgver}
    ./configure \
        --prefix="/opt/${_pkgname}" \
        --with-random=/dev/urandom \
        --disable-ldaps \
        --disable-ldap \
        --enable-manual \
        --disable-versioned-symbols \
        --enable-threaded-resolver \
        --with-ca-bundle=/etc/ssl/certs/ca-certificates.crt \
        --with-gnutls \
        --without-libidn
    make
}

package() {
    cd ${_pkgname}-${pkgver}
    make DESTDIR=${pkgdir} install
    ln -s libcurl.so.4 ${pkgdir}/opt/${_pkgname}/lib/libcurl-gnutls.so.4
    install -Dm644 COPYING ${pkgdir}/opt/${_pkgname}/share/licenses/${_pkgname}/COPYING
    install -Dm644 docs/libcurl/libcurl.m4 ${pkgdir}/opt/${_pkgname}/share/aclocal/libcurl.m4
}
