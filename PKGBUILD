# Maintainer: Daniel Wallace <daniel.wallace at gatech dot edu>
pkgname=gdrive-cli-git
_pkgname=gdrive-cli
pkgver=20120428
pkgrel=3
pkgdesc="google drive cli - futher instructions to come tomorrow, follow the read me for now"
arch=("any")
url="http://tomdignan.com/projects/gdrive-cli/"
license=('GPL')
depends=('python2-google-api-python-client' 'python2-httplib2' 'sqlite')
makedepends=('git')
source=('client_secrets.json'
        'gdrive-cli')

_gitroot=https://github.com/tom-dignan/gdrive-cli.git
_gitname=gdrive

build() {
  cd "$srcdir"
  msg "Connecting to GIT server...."

  if [[ -d "$_gitname" ]]; then
    cd "$_gitname" && git pull origin
    msg "The local files are updated."
  else
    git clone "$_gitroot" "$_gitname"
  fi

  msg "GIT checkout done or server timeout"
  msg "Starting build..."

  rm -rf "$srcdir/$_gitname-build"

  git clone "$srcdir/$_gitname" "$srcdir/$_gitname-build"

  cd "$srcdir/$_gitname-build"
  mkdir .private
  ln -s "$srcdir/client_secrets.json .private/client_secrets.json"
  #python2 setup.py build
  sed -i 's/python/&2/g' $(find -type f)
}

package() {
  cd "$srcdir/$_gitname-build"
  install -d "$pkgdir/usr/share/gdrive-cli"
  cp -dpr --no-preserve=ownership * "$pkgdir/usr/share/gdrive-cli/"
  #ln -s $pkgdir/usr/share/gdrive-cli/gdrive-cli.py $pkgdir/usr/bin/gdrive-cli
  install -Dm755 "$srcdir/gdrive-cli" "$pkgdir/usr/bin/gdrive-cli"
  install -Dm644 "$startdir/client_secrets.json" "$pkgdir/etc/gdrive-client"
}

md5sums=('727e9422ae2827c94b442f94b1670141'
         'd592ad2db6bd5d9dd203063b5909285b')
# vim:set ts=2 sw=2 filetype=PKGBUILD
