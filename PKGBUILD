# Maintainer: hiddeninthesand <hiddeninthesand at pm dot me>

pkgname="podman"
_gitname="podman"
provides=('podman')
pkgver='4.7.2'
pkgrel='1'
pkgdesc="A tool for managing OCI containers and pods."
arch=("amd64")
url="https://podman.io/"
license=('Apache')
makedepends=(
    'golang-go>=2:1.18.0'
    'pkg-config'
    'git'
    'libbtrfs-dev'
    'libsystemd-dev'
    'libdevmapper-dev'
    'libgpgme-dev'
    'libseccomp-dev'
    ) # 'libapparmor-dev' 'libassuan-dev' 'libc6-dev' 'libglib2.0-dev' 'libgpg-error-dev' 'libprotobuf-dev' 'libprotobuf-c-dev' 'libselinux1-dev'
depends=(
    'systemd'
    'conmon>=2.1.5'
    'crun'
    'golang-github-containers-common'
    'libc6'
    'libdevmapper1.02.1'
    'libgpgme11'
    'libseccomp2'
    'libsubid4'
    )
source=("git+https://github.com/containers/podman.git#tag=v${pkgver}")
optdepends=(
    's!btrfs-progs: support btrfs backend devices'
    'r!buildah: CLI tool to facilitate building OCI images'
    'r!catatonit: init process for containers'
    'r!dbus-user-session: simple interprocess messaging system (systemd--user integration)'
    'r!fuse-overlayfs>=1.0.0~: implementaion of overlay+shiftfs in FUSE for rootless containers'
    'r!slirp4netns: User-mode networking for unpriviledged network namespaces'
    'r!uidmap: programs to help use subuids'
    's!containers-storage: CLI tools for handling how containers are stored on disk'
    's!podman-compose: for docker-compose compatibility'
    's!podman-docker: for Docker-compatible CLI'
    's!iptables: administration tool for packet filtering and NAT'
  )

b2sums=('SKIP')
conflicts=("${_gitname}-git" "${_gitname}-bin")

build() {
	cd ${_gitname}
	make BUILDTAGS="selinux seccomp systemd apparmor"
}

package() {
	# installing binaries
	cd ${_gitname}
	make install PREFIX="${pkgdir}/usr"
}
