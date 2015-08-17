# Maintainer: count-corrupt <corrupt at giggedy dot de>
pkgname=rr231x_0x
pkgver=2.5
pkgrel=1
pkgdesc="Kernel modules for Highpoint RocketRAID 230x and 231x SATA cards. Patched for use with kernel26 =2.6.37, >=2.6.38 and kernel >= 3 (a.k.a. linux)"
arch=('i686' 'x86_64')
url="http://www.highpoint-tech.com/USA/bios_rr2310.htm"
license=('custom')
groups=()

if [[ `uname -r` == 2.6.* ]]; then
depends=('kernel26')
makedepends=('kernel26-headers')
else
depends=('linux')
makedepends=('linux-headers')
fi

provides=()
conflicts=()
replaces=()
backup=()
options=()
install=$pkgname.install
source=(http://www.highpoint-tech.cn/BIOS_Driver/rr231x_00/Linux/$pkgname-linux-src-v$pkgver-091022-1618.tar.gz
 scsi_lck.patch kernel3.patch)
noextract=()
md5sums=('59ce7354ed06f780584fed124c57c222' 'aab69de268d55cba45520403c675c0fe' '17f4e6ac04625a4ed25d720cdfab674d')

#_kernver=3.0-ARCH
_kernver=`uname -r`

build() {
    mkdir -p $startdir/pkg/lib/modules/${_kernver}/kernel/drivers/scsi/

    # Apply the scsi lock patch to make the driver work with kernel26 > 2.6.37
    cd $startdir
    patch -p0 -i $startdir/scsi_lck.patch
	patch -p0 -i $startdir/kernel3.patch

    cd $startdir/src/$pkgname-linux-src-v$pkgver/product/rr2310pm/linux/
    make KERNELDIR=/usr/src/linux-$_kernver || return 1

    # Install the kernel module
    install -m 644 -D rr2310_00.ko $startdir/pkg/lib/modules/${_kernver}/kernel/drivers/scsi/

    mkdir -p $startdir/pkg/usr/share/licenses/$pkgname
    cp $startdir/src/$pkgname-linux-src-v$pkgver/README $startdir/pkg/usr/share/licenses/$pkgname/
}
 

