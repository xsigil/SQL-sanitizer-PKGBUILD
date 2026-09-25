# Maintainer: Your Name <your.email@example.com>
pkgname=sql-sanitizer
pkgver=0.1.0
pkgrel=1
pkgdesc="Ultra-fast, zero-ORM, injection-safe text-to-SQLite stream filter in Bison/C"
arch=('x86_64' 'aarch64')
url="https://github.com/xsigil/SQL-sanitizer"
license=('MIT')
depends=('glibc')
makedepends=('bison' 'gcc')
checkdepends=('sqlite')
# For release tarballs:
source=("$pkgname-$pkgver.tar.gz::$url/archive/refs/tags/v$pkgver.tar.gz")
sha256sums=('SKIP')

build() {
    cd "SQL-sanitizer-$pkgver"
    make CFLAGS="$CFLAGS -std=c99"
}

check() {
    cd "SQL-sanitizer-$pkgver"
    make test
}

package() {
    cd "SQL-sanitizer-$pkgver"

    # Install binary
    install -Dm755 bin/sql_filter "$pkgdir/usr/bin/sql_filter"

    # Install manual page (makepkg will automatically compress to .gz)
    if [ -f "doc/sql_filter.1" ]; then
        install -Dm644 doc/sql_filter.1 "$pkgdir/usr/share/man/man1/sql_filter.1"
    elif [ -f "man/sql_filter.1" ]; then
        install -Dm644 man/sql_filter.1 "$pkgdir/usr/share/man/man1/sql_filter.1"
    fi

    # Install license if available
    if [ -f "LICENSE" ]; then
        install -Dm644 LICENSE "$pkgdir/usr/share/licenses/$pkgname/LICENSE"
    fi
}
