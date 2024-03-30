pkgname=file-manager-git
_pkgname=file-manager
pkgver=r6.6f72553
pkgrel=1
pkgdesc='Tree-based terminal file manager'
makedepends=('git' 'cargo')
arch=('x86_64')
url="https://github.com/dcompoze/file-manager"
license=('MIT')
source=("${_pkgname}"::"git+${url}")
sha256sums=('SKIP')
provides=("${_pkgname}")
conflicts=("${_pkgname}")

pkgver() {
	cd "${srcdir}/${_pkgname}"
	printf "r%s.%s" "$(git rev-list --count HEAD)" "$(git rev-parse --short HEAD)"
}

prepare() {
	cd "${srcdir}/${_pkgname}"
	cargo update
	cargo fetch --locked --target "$CARCH-unknown-linux-gnu"
}

build() {
	cd "${srcdir}/${_pkgname}"
	RUSTUP_TOOLCHAIN=stable cargo build --release --frozen --target-dir=target
}

#check() {
#	cd "${srcdir}/${_pkgname}"
#	RUSTUP_TOOLCHAIN=stable cargo test --frozen
#}

package() {
	cd "${srcdir}/${_pkgname}"
	install -Dm755 -t "${pkgdir}/usr/bin" "./target/release/fm"
	install -Dm755 -t "${pkgdir}/usr/bin" "./target/release/fm-server"
	install -Dm644 ./desktop/icons/file-manager-16x16.png "${pkgdir}/usr/share/icons/hicolor/16x16/apps/file-manager.png"
	install -Dm644 ./desktop/icons/file-manager-32x32.png "${pkgdir}/usr/share/icons/hicolor/32x32/apps/file-manager.png"
	install -Dm644 ./desktop/icons/file-manager-256x256.png "${pkgdir}/usr/share/icons/hicolor/256x256/apps/file-manager.png"
	install -Dm644 ./desktop/icons/file-manager-512x512.png "${pkgdir}/usr/share/icons/hicolor/512x512/apps/file-manager.png"
	install -Dm644 -t "${pkgdir}/usr/share/man/man1" ./desktop/man/fm.1
	install -Dm644 -t "${pkgdir}/usr/share/applications" ./desktop/fm.desktop
	install -Dm644 ./desktop/fm.zsh "${pkgdir}/usr/share/zsh/site-functions/_fm"
}
