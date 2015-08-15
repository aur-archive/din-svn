# Contributor: SpepS <dreamspepser at yahoo dot it>

pkgname=din-svn
pkgver=2214
pkgrel=1
pkgdesc="A software musical instrument and audio synthesizer that let you use multiple Bezier curves to draw and sculpt waveforms"
arch=('i686' 'x86_64')
url="http://dinisnoise.org/"
license=('GPL')
depends=('liblo' 'libgl' 'libircclient' 'tcl' 'jack' 'sdl' 'fftw')

_svntrunk="http://din.googlecode.com/svn/trunk/"
_svnmod="din"

build() {

  cd ${srcdir}

  if [ -d $_svnmod ] ; then
    (cd $_svnmod && svn update)
    msg "The local files are updated."
  else
    svn co ${_svntrunk} ${_svnmod}
  fi

  cd $srcdir/$_svnmod

  # Fix share dir
  sed -i "s|var/|share/|" data/checkdotdin

  # Fix tcl include dir
  sed -i "s|tcl8.5/||g" configure*

  ./configure --prefix=/usr --localstatedir=/usr/share

  make
}

package() {
  cd $srcdir/$_svnmod

  make DESTDIR="$pkgdir/" install
}

# vim:set ts=2 sw=2 et:
