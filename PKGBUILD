# Maintainer: Myles English <myles at rockhead dot biz>
pkgname=instant-bzr
pkgver=344
pkgrel=1
pkgdesc="A Python module allowing for instant inlining of C and C++ code in Python"
arch=('any')
url="http://launchpad.net/instant"
license=('LGPL')
groups=('fenics-bzr')
depends=('python2' 'swig')
conflicts=('instant')
provides=('instant')
options=(!emptydirs)

_bzrtrunk=lp:instant
_bzrmod=instant

build() {
    msg "Connecting to Bazaar server...."

    if [ -d $_bzrmod ]; then
	cd $_bzrmod && bzr pull $_bzrtrunk -r $pkgver && cd ..
	msg "The local files are updated."
    else
	bzr branch $_bzrtrunk $_bzrmod -r $pkgver
    fi

    msg "BZR checkout done or server timeout"
    msg "Starting make..."

    [ -d $_bzrmod-build ] && rm -rf $_bzrmod-build
    cp -r $_bzrmod $_bzrmod-build
    cd $_bzrmod-build

    find ./ -name "*" -type f -exec \
	sed -i 's#\(/usr/bin/env \|/usr/bin/\)python[2-3]*#\1python2#' {} \;

    #find ./ -name "*" -type f -exec \
    #   sed -i '/-python /! {s/python /python2 /}' {} \;

    python2 setup.py build
}

package() {
  cd $srcdir/$_bzrmod-build
  python2 setup.py install --root=$pkgdir
}

# vim:set ts=2 sw=2 et:
