# Maintainer: Sylvain POULAIN <sylvain.poulain@giscan.com>

pkgname=beremiz
pkgver=1.0
pkgrel=1
pkgdesc="Beremiz is an integrated development environment for machine automation. It is Free Software, conforming to IEC-61131 among other standards"
arch=('i686' 'x86_64')
makedepends=('python2-pyro' 'python2-matplotlib' 'python-nevow' 'python2-lxml' 'mercurial' 'wxgtk3')
url="https://github.com/nucleron/beremiz"
license=('GPLv2')
#source=("https://github.com/nucleron/beremiz/archive/master.zip")
#md5sums=('c65ff52604c9799627b7db62a1e8e62b')

build() {
	mkdir -p beremiz
	cd "$srcdir/beremiz"
	
	hg clone https://bitbucket.org/skvorl/beremiz
	hg clone https://bitbucket.org/mjsousa/matiec
	#hg clone http://dev.automforge.net/CanFestival-3
	
	cd "$srcdir/beremiz/matiec"
	autoreconf -i
	./configure
	make
	
	#cd "$srcdir/beremiz/CanFestival-3"
	#./configure --can=virtual
	#make -j1
	
}

_pkgprefix='opt/beremiz'

package() {
  mkdir -p $pkgdir/usr/bin
  echo "#!/bin/sh" > $pkgdir/usr/bin/$pkgname
  echo "python2 /$_pkgprefix/beremiz/Beremiz.py" >> $pkgdir/usr/bin/$pkgname
  chmod 755 $pkgdir/usr/bin/$pkgname

  for size in "16x16" "32x32" "48x48" "64x64" "128x128"
  do
    install -Dm644 "${srcdir}/${pkgname}/${pkgname}/images/brz.png" $pkgdir/usr/share/icons/hicolor/$size/apps/$pkgname.png
  done
  
	mkdir -p $pkgdir/usr/share/applications
	echo "[Desktop Entry]" > $pkgdir/usr/share/applications/$pkgname.desktop
	echo "Type=Application" >> $pkgdir/usr/share/applications/$pkgname.desktop
	echo "Name=Beremiz" >> $pkgdir/usr/share/applications/$pkgname.desktop
	echo "Comment=Machine automation" >> $pkgdir/usr/share/applications/$pkgname.desktop
	echo "Exec=python2 /opt/beremiz/beremiz/Beremiz.py" >> $pkgdir/usr/share/applications/$pkgname.desktop
	echo "Icon=$pkgdir/usr/share/icons/hicolor/$size/apps/$pkgname.png" >> $pkgdir/usr/share/applications/$pkgname.desktop
	echo "Terminal=false" >> $pkgdir/usr/share/applications/$pkgname.desktop
	echo "Categories=Graphics;2DGraphics;" >> $pkgdir/usr/share/applications/$pkgname.desktop	
	chmod 755 $pkgdir/usr/share/applications/$pkgname.desktop

  # Install Draftsight's program files
  mkdir -p $pkgdir/$_pkgprefix/
  cp -pr $srcdir/$pkgname/* $pkgdir/$_pkgprefix/
}
