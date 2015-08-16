pkgname=nedetlesmaki
pkgver=r1143.1eb057c
pkgrel=1
pkgdesc='Puzzle game with isometric 3d graphics inspired by Sokoban'
arch=('i686', 'x86_64')
license=('MIT' 'FAL')
url="http://geekygoblin.org/ned-et-les-maki/"
depends=('java-runtime')
makedepends=('maven' 'git')
source=("git+https://github.com/devnewton/nedetlesmaki.git")
md5sums=('SKIP')

pkgver() {
  cd "$srcdir/nedetlesmaki"
  printf "r%s.%s" "$(git rev-list --count HEAD)" "$(git rev-parse --short HEAD)"
}

build()
{
  cd "$srcdir/nedetlesmaki"
  mvn package
}

package ()
{
  cd "$srcdir/nedetlesmaki"
  install -d "$pkgdir"/usr/bin
  install -d "$pkgdir"/usr/share/java/nedetlesmaki
  install -m644 core/target/nedetlesmaki-*.jar "$pkgdir"/usr/share/java/nedetlesmaki
  install -m644 packages/generic/target/lib/*.jar "$pkgdir"/usr/share/java/nedetlesmaki
  cp -r assets packages/generic/target/natives "$pkgdir"/usr/share/java/nedetlesmaki
  echo "#!/bin/sh" > run
  echo 'exec "$JAVA_HOME/bin/java" -Djava.library.path=/usr/share/java/nedetlesmaki/natives -jar `ls /usr/share/java/nedetlesmaki/nedetlesmaki-lwjgl-*.jar` "$@"' >> run
  install -m755 run "$pkgdir"/usr/bin/nedetlesmaki
  install -D -m644 packages/deb/src/launchers/nedetlesmaki.desktop "$pkgdir"/usr/share/applications/nedetlesmaki.desktop
  sed -i "s|/opt/nedetlesmaki|/usr/share/java/nedetlesmaki|g" "$pkgdir"/usr/share/applications/nedetlesmaki.desktop
}
