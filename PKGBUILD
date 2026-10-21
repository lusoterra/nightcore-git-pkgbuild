# Maintainer: Lev <lev@lusosterone.net>
pkgname=nightcore-git
_pkgname=nightcore
pkgver=r64.gc5fa974
pkgrel=1
pkgdesc="Bit-perfect nightcore/speed/pitch audio tool (ffmpeg, sox, rubberband)"
arch=('any')
url="https://git.lusosterone.net/lev/nightcore"
license=('MIT')
depends=(
  'python'
  'python-mutagen'
  'ffmpeg'
  'sox'
  'rubberband'
  'flac'
  'opus-tools'
  'vorbis-tools'
)
optdepends=(
  'lame: preferred MP3 encoder (ffmpeg libmp3lame fallback)'
  'qaac-wine: High-quality AAC/ALAC encoding (CoreAudio via Wine)'
  'bash-completion: bash completion'
  'zsh: zsh completion'
  'fish: fish completion'
)
makedepends=('git' 'python-build' 'python-installer' 'python-setuptools')
provides=("$_pkgname")
conflicts=("$_pkgname")
source=("$_pkgname::git+$url")
sha256sums=('SKIP')

pkgver() {
  cd "$_pkgname"
  printf "r%s.g%s\n" \
    "$(git rev-list --count HEAD)" \
    "$(git rev-parse --short HEAD)"
}

build() {
  cd "$_pkgname"
  python -m build --wheel --no-isolation
}

package() {
  cd "$_pkgname"
  python -m installer --destdir="$pkgdir" dist/*.whl
  install -Dm644 completions/nightcore.bash "$pkgdir/usr/share/bash-completion/completions/nightcore"
  install -Dm644 completions/_nightcore "$pkgdir/usr/share/zsh/site-functions/_nightcore"
  install -Dm644 completions/nightcore.fish "$pkgdir/usr/share/fish/vendor_completions.d/nightcore.fish"
  install -Dm644 nightcore.1 "$pkgdir/usr/share/man/man1/nightcore.1"
  install -Dm644 LICENSE "$pkgdir/usr/share/licenses/$pkgname/LICENSE"
}
