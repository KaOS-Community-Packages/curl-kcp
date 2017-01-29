pkgname=curl-kcp
_pkgname=curl
pkgver=7.52.1
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
md5sums=('dd014df06ff1d12e173de86873f9f77a')

build() {
    cd ${_pkgname}-${pkgver}
    ./configure \
        --prefix=/opt/${_pkgname} \
        --with-random=/dev/urandom \
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
    install -dm755 ${pkgdir}/opt/${_pkgname}
    mkdir -p ${pkgdir}/opt/${_pkgname}/share/{licenses/${_pkgname},aclocal}
    cd ${_pkgname}-${pkgver}
    make DESTDIR=${pkgdir} install
    install -Dm644 COPYING ${pkgdir}/opt/${_pkgname}/share/licenses/${_pkgname}/COPYING
    install -Dm644 docs/libcurl/libcurl.m4 ${pkgdir}/opt/${_pkgname}/share/aclocal/libcurl.m4
}