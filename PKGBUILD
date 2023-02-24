# Maintainer: hiddeninthesand <hiddeninthesand at pm dot me>

pkgname="podman"
_gitname="podman"
provides=('podman')
pkgver='4.4.2'
pkgrel='1'
pkgdesc="A tool for managing OCI containers and pods."
arch=("amd64")
url="https://podman.io/"
license=('Apache')
makedepends=('golang-go>=1.16.0' 'pkg-config' 'git')
depends=('slirp4netns' 'systemd' 'libapparmor-dev' 'conmon>=2.1.5' 'btrfs-progs' 'runc' 'go-md2man' 'iptables' 'libassuan-dev' 'libbtrfs-dev' 'libc6-dev' 'libdevmapper-dev' 'libglib2.0-dev' 'libgpgme-dev' 'libgpg-error-dev' 'libprotobuf-dev' 'libprotobuf-c-dev' 'libseccomp-dev' 'libselinux1-dev' 'libsystemd-dev' 'uidmap')
source=("git+https://github.com/containers/podman.git#tag=v${pkgver}"
		"https://src.fedoraproject.org/rpms/containers-common/raw/main/f/registries.conf"
		"https://src.fedoraproject.org/rpms/containers-common/raw/main/f/default-policy.json")
b2sums=('SKIP'
        '0cb5f1e8b30a48b337bea4effcad172d3c379ccde4fa89d500cfffd6e8bf017f22664e923f53584d6322662a966bddf584f2298c9aae464a33e4bdb1f399f792'
        '9b4d41f6063ff6131648d801ad44951f3a426551deb5a6d3ea4f991339d5f375f003fffcf637632c9d83b1e74eda959750906316a1c510c728cf8a93548d4cf8')
conflicts=("${_gitname}-git" "${_gitname}-bin")
backup=('/etc/containers/registries.conf'
		'/etc/containers/policy.json')

build() {
	cd ${_gitname}
	make BUILDTAGS="selinux seccomp systemd apparmor"
}

package() {
	# installing config
	install -Dm644 "registries.conf" "${pkgdir}/etc/containers/registries.conf"
	install -Dm644 "default-policy.json" "${pkgdir}/etc/containers/policy.json"
	# installing binaries
	cd ${_gitname}
	make install PREFIX="${pkgdir}/usr"
}
