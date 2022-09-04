# Maintainer:   echo -n 'TWF0dCBDLiA8bWF0dEBnZXRjcnlzdC5hbD4='     | base64 -d
# Maintainer:   echo -n 'TWljaGFsIFMuIDxtaWNoYWxAZ2V0Y3J5c3QuYWw+' | base64 -d
# Contributor:  echo -n 'TWljaGFsIFMuIDxtaWNoYWxAZ2V0Y3J5c3QuYWw+' | base64 -d

pkgname=malachite
pkgver=2.0.0
pkgrel=1
pkgdesc="Tool for packaging and maintaining pacman repositories"
arch=('x86_64' 'aarch64')
url="https://github.com/crystal-linux/$pkgname"
license=('GPL3')
source=("git+$url?rev=v$pkgver")
sha256sums=('SKIP')
depends=('git' 'pacman-contrib' 'gnupg')
makedepends=('cargo')

prepare() {
    cd "$srcdir/$pkgname"
    cargo fetch --locked --target "$CARCH-unknown-linux-gnu"
}

build() {
    cd "$srcdir/$pkgname"
    export RUSTUP_TOOLCHAIN=stable
    export CARGO_TARGET_DIR=target
    cargo build --frozen --release --all-features
}

package() {
    cd "$srcdir/$pkgname"
    find target/release \
        -maxdepth 1 \
        -executable \
        -type f \
        -exec install -Dm0755 -t "${pkgdir}/usr/bin" {} +
}