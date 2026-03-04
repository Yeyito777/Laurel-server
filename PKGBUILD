# Maintainer: Yeyito <yeyito@yeyito.dev>
pkgname=laurel-server-git
pkgver=r0
pkgrel=1
pkgdesc='Laurel clip server — nginx-based video clip hosting'
arch=('any')
url='https://github.com/Yeyito777/Laurel-server'
license=('MIT')
depends=('nginx' 'ffmpeg')
optdepends=(
    'certbot: HTTPS certificate management'
    'certbot-nginx: certbot nginx plugin'
)
makedepends=('git')
provides=('laurel-server')
conflicts=('laurel-server')
install=laurel-server.install
backup=('etc/nginx/sites-available/laurel.conf')
source=('git+https://github.com/Yeyito777/Laurel-server.git')
sha256sums=('SKIP')

pkgver() {
    cd Laurel-server
    printf "r%s.%s" "$(git rev-list --count HEAD)" "$(git rev-parse --short HEAD)"
}

package() {
    cd Laurel-server
    install -Dm644 laurel.nginx.conf "$pkgdir/etc/nginx/sites-available/laurel.conf"
    install -Dm644 index.html "$pkgdir/usr/share/laurel-server/index.html"
    install -Dm644 post-receive "$pkgdir/usr/share/laurel-server/post-receive"
    install -dm755 "$pkgdir/srv/clips"
}
