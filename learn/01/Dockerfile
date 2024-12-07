#
# NOTE: THIS DOCKERFILE IS GENERATED VIA "apply-templates.sh"
#
# PLEASE DO NOT EDIT IT DIRECTLY.
#

FROM buildpack-deps:bullseye
# Step 1/9 : FROM buildpack-deps:bullseye

RUN set -ex; \
	if ! command -v gpg > /dev/null; then \
		apt-get update; \
		apt-get install -y --no-install-recommends \
			gnupg \
			dirmngr \
		; \
		rm -rf /var/lib/apt/lists/*; \
	fi
# Step 2/9 : RUN
# set -ex;
# if ! command -v gpg > /dev/null; then
# 	apt-get update;
# 	apt-get install -y --no-install-recommends gnupg dirmngr;
# 	rm -rf /var/lib/apt/lists/*;
# fi

# https://gcc.gnu.org/mirrors.html
ENV GPG_KEYS \
# 1024D/745C015A 1999-11-09 Gerald Pfeifer <gerald@pfeifer.com>
	B215C1633BCA0477615F1B35A5B3A004745C015A \
# 1024D/B75C61B8 2003-04-10 Mark Mitchell <mark@codesourcery.com>
	B3C42148A44E6983B3E4CC0793FA9B1AB75C61B8 \
# 1024D/902C9419 2004-12-06 Gabriel Dos Reis <gdr@acm.org>
	90AA470469D3965A87A5DCB494D03953902C9419 \
# 1024D/F71EDF1C 2000-02-13 Joseph Samuel Myers <jsm@polyomino.org.uk>
	80F98B2E0DAB6C8281BDF541A7C8C3B2F71EDF1C \
# 2048R/FC26A641 2005-09-13 Richard Guenther <richard.guenther@gmail.com>
	7F74F97C103468EE5D750B583AB00996FC26A641 \
# 1024D/C3C45C06 2004-04-21 Jakub Jelinek <jakub@redhat.com>
	33C235A34C46AA3FFB293709A328C3A2C3C45C06 \
# 4096R/09B5FA62 2020-05-28 Jakub Jelinek <jakub@redhat.com>
	D3A93CAD751C2AF4F8C7AD516C35B99309B5FA62
# Step 3/9 : ENV GPG_KEYS B215C1633BCA0477615F1B35A5B3A004745C015A B3C42148A44E6983B3E4CC0793FA9B1AB75C61B8 90AA470469D3965A87A5DCB494D03953902C9419 80F98B2E0DAB6C8281BDF541A7C8C3B2F71EDF1C 7F74F97C103468EE5D750B583AB00996FC26A641 33C235A34C46AA3FFB293709A328C3A2C3C45C06 D3A93CAD751C2AF4F8C7AD516C35B99309B5FA62

RUN set -ex; \
	for key in $GPG_KEYS; do \
		gpg --batch --keyserver keyserver.ubuntu.com --recv-keys "$key"; \
	done
# Step 4/9 : RUN
# set -ex;
# for key in $GPG_KEYS; do
# 	gpg --batch --keyserver keyserver.ubuntu.com --recv-keys "$key";
# done
# + gpg --batch --keyserver keyserver.ubuntu.com --recv-keys B215C1633BCA0477615F1B35A5B3A004745C015A
# + gpg --batch --keyserver keyserver.ubuntu.com --recv-keys B3C42148A44E6983B3E4CC0793FA9B1AB75C61B8
# + gpg --batch --keyserver keyserver.ubuntu.com --recv-keys 90AA470469D3965A87A5DCB494D03953902C9419
# + gpg --batch --keyserver keyserver.ubuntu.com --recv-keys 80F98B2E0DAB6C8281BDF541A7C8C3B2F71EDF1C
# + gpg --batch --keyserver keyserver.ubuntu.com --recv-keys 7F74F97C103468EE5D750B583AB00996FC26A641
# + gpg --batch --keyserver keyserver.ubuntu.com --recv-keys 33C235A34C46AA3FFB293709A328C3A2C3C45C06
# + gpg --batch --keyserver keyserver.ubuntu.com --recv-keys D3A93CAD751C2AF4F8C7AD516C35B99309B5FA62

# https://gcc.gnu.org/mirrors.html
ENV GCC_MIRRORS \
		https://ftpmirror.gnu.org/gcc \
		https://mirrors.kernel.org/gnu/gcc \
		https://bigsearcher.com/mirrors/gcc/releases \
		http://www.netgull.com/gcc/releases \
		https://ftpmirror.gnu.org/gcc \
# only attempt the origin FTP as a mirror of last resort
		ftp://ftp.gnu.org/gnu/gcc
# Step 5/9 : ENV GCC_MIRRORS https://ftpmirror.gnu.org/gcc https://mirrors.kernel.org/gnu/gcc https://bigsearcher.com/mirrors/gcc/releases http://www.netgull.com/gcc/releases https://ftpmirror.gnu.org/gcc ftp://ftp.gnu.org/gnu/gcc

# Last Modified: 2022-08-19
ENV GCC_VERSION 12.2.0
# Docker EOL: 2024-02-19
# Step 6/9 : ENV GCC_VERSION 12.2.0

RUN set -ex; \
	\
	savedAptMark="$(apt-mark showmanual)"; \
	apt-get update; \
	apt-get install -y --no-install-recommends \
		dpkg-dev \
		flex \
	; \
	rm -r /var/lib/apt/lists/*; \
	\
	_fetch() { \
		local fetch="$1"; shift; \
		local file="$1"; shift; \
		for mirror in $GCC_MIRRORS; do \
			if curl -fL "$mirror/$fetch" -o "$file"; then \
				return 0; \
			fi; \
		done; \
		echo >&2 "error: failed to download '$fetch' from several mirrors"; \
		return 1; \
	}; \
	\
	_fetch "gcc-$GCC_VERSION/gcc-$GCC_VERSION.tar.xz.sig" 'gcc.tar.xz.sig'; \
	_fetch "gcc-$GCC_VERSION/gcc-$GCC_VERSION.tar.xz" 'gcc.tar.xz'; \
	gpg --batch --verify gcc.tar.xz.sig gcc.tar.xz; \
	mkdir -p /usr/src/gcc; \
	tar -xf gcc.tar.xz -C /usr/src/gcc --strip-components=1; \
	rm gcc.tar.xz*; \
	\
	cd /usr/src/gcc; \
	\
# "download_prerequisites" pulls down a bunch of tarballs and extracts them,
# but then leaves the tarballs themselves lying around
	./contrib/download_prerequisites; \
	{ rm *.tar.* || true; }; \
	\
# explicitly update autoconf config.guess and config.sub so they support more arches/libcs
	for f in config.guess config.sub; do \
		wget -O "$f" "https://git.savannah.gnu.org/cgit/config.git/plain/$f?id=7d3d27baf8107b630586c962c057e22149653deb"; \
# find any more (shallow) copies of the file we grabbed and update them too
		find -mindepth 2 -name "$f" -exec cp -v "$f" '{}' ';'; \
	done; \
	\
	dir="$(mktemp -d)"; \
	cd "$dir"; \
	\
	extraConfigureArgs=''; \
	dpkgArch="$(dpkg --print-architecture)"; \
	case "$dpkgArch" in \
# with-arch: https://salsa.debian.org/toolchain-team/gcc/-/blob/gcc-11-debian/debian/rules2#L462-502
# with-float: https://salsa.debian.org/toolchain-team/gcc/-/blob/gcc-11-debian/debian/rules.defs#L502-512
# with-mode: https://salsa.debian.org/toolchain-team/gcc/-/blob/gcc-11-debian/debian/rules.defs#L480
		armel) \
			extraConfigureArgs="$extraConfigureArgs --with-arch=armv5te --with-float=soft" \
			;; \
		armhf) \
			# https://bugs.launchpad.net/ubuntu/+source/gcc-defaults/+bug/1939379/comments/2
			extraConfigureArgs="$extraConfigureArgs --with-arch=armv7-a+fp --with-float=hard --with-mode=thumb" \
			;; \
		\
# with-arch-32: https://salsa.debian.org/toolchain-team/gcc/-/blob/gcc-11-debian/debian/rules2#L598
		i386) \
			extraConfigureArgs="$extraConfigureArgs --with-arch-32=i686"; \
			;; \
	esac; \
	\
	gnuArch="$(dpkg-architecture --query DEB_BUILD_GNU_TYPE)"; \
	/usr/src/gcc/configure \
		--build="$gnuArch" \
		--disable-multilib \
		--enable-languages=c,c++,fortran,go \
		$extraConfigureArgs \
	; \
	make -j "$(nproc)"; \
	make install-strip; \
	\
	cd ..; \
	\
	rm -rf "$dir" /usr/src/gcc; \
	\
	apt-mark auto '.*' > /dev/null; \
	[ -z "$savedAptMark" ] || apt-mark manual $savedAptMark; \
	apt-get purge -y --auto-remove -o APT::AutoRemove::RecommendsImportant=false

# Step 7/9 : RUN
# set -ex;
# savedAptMark="$(apt-mark showmanual)";
# apt-get update;
# apt-get install -y --no-install-recommends dpkg-dev flex;
# rm -r /var/lib/apt/lists/*;
# _fetch() {
# 	local fetch="$1"; shift;
# 	local file="$1"; shift;
# 	for mirror in $GCC_MIRRORS; do
# 		if curl -fL "$mirror/$fetch" -o "$file"; then
# 			return 0;
# 		fi;
# 	done; echo >&2 "error: failed to download '$fetch' from several mirrors";
# 	return 1;
# };
# _fetch "gcc-$GCC_VERSION/gcc-$GCC_VERSION.tar.xz.sig" 'gcc.tar.xz.sig';
# _fetch "gcc-$GCC_VERSION/gcc-$GCC_VERSION.tar.xz" 'gcc.tar.xz';
# gpg --batch --verify gcc.tar.xz.sig gcc.tar.xz;
# mkdir -p /usr/src/gcc;
# tar -xf gcc.tar.xz -C /usr/src/gcc --strip-components=1;
# rm gcc.tar.xz*;
# cd /usr/src/gcc;
# ./contrib/download_prerequisites;
# { rm *.tar.* || true; };
# for f in config.guess config.sub; do
# 	wget -O "$f" "https://git.savannah.gnu.org/cgit/config.git/plain/$f?id=7d3d27baf8107b630586c962c057e22149653deb";
# 	find -mindepth 2 -name "$f" -exec cp -v "$f" '{}' ';';
# done;
# dir="$(mktemp -d)";
# cd "$dir";
# extraConfigureArgs='';
# dpkgArch="$(dpkg --print-architecture)";
# case "$dpkgArch" in
# 	armel)
# 		extraConfigureArgs="$extraConfigureArgs --with-arch=armv5te --with-float=soft"
# 		;;
# 	armhf)
# 		extraConfigureArgs="$extraConfigureArgs --with-arch=armv7-a+fp --with-float=hard --with-mode=thumb"
# 		;;
# 	i386)
# 		extraConfigureArgs="$extraConfigureArgs --with-arch-32=i686";
# 		;;
# esac;
# gnuArch="$(dpkg-architecture --query DEB_BUILD_GNU_TYPE)";
# /usr/src/gcc/configure --build="$gnuArch" --disable-multilib --enable-languages=c,c++,fortran,go $extraConfigureArgs;
# make -j "$(nproc)";
# make install-strip;
# cd ..;
# rm -rf "$dir" /usr/src/gcc;
# apt-mark auto '.*' > /dev/null;
# [ -z "$savedAptMark" ] || apt-mark manual $savedAptMark;
# apt-get purge -y --auto-remove -o APT::AutoRemove::RecommendsImportant=false


# + apt-mark showmanual
# + savedAptMark=autoconf
# automake
# bzip2
# ca-certificates
# curl
# default-libmysqlclient-dev
# dpkg-dev
# file
# g++
# gcc
# git
# gnupg
# imagemagick
# libbz2-dev
# libc6-dev
# libcurl4-openssl-dev
# libdb-dev
# libevent-dev
# libffi-dev
# libgdbm-dev
# libglib2.0-dev
# libgmp-dev
# libjpeg-dev
# libkrb5-dev
# liblzma-dev
# libmagickcore-dev
# libmagickwand-dev
# libmaxminddb-dev
# libncurses5-dev
# libncursesw5-dev
# libpng-dev
# libpq-dev
# libreadline-dev
# libsqlite3-dev
# libssl-dev
# libtool
# libwebp-dev
# libxml2-dev
# libxslt1-dev
# libyaml-dev
# make
# mercurial
# netbase
# openssh-client
# patch
# procps
# subversion
# unzip
# wget
# xz-utils
# zlib1g-dev
# + apt-get update
# Get:1 http://deb.debian.org/debian bullseye InRelease [116 kB]
# Get:2 http://deb.debian.org/debian-security bullseye-security InRelease [48.4 kB]
# Get:3 http://deb.debian.org/debian bullseye-updates InRelease [44.1 kB]
# Get:4 http://deb.debian.org/debian bullseye/main amd64 Packages [8062 kB]
# Get:5 http://deb.debian.org/debian-security bullseye-security/main amd64 Packages [257 kB]
# Get:6 http://deb.debian.org/debian bullseye-updates/main amd64 Packages [17.4 kB]
# Fetched 8545 kB in 13min 38s (10.4 kB/s)
# Reading package lists...
# + apt-get install -y --no-install-recommends dpkg-dev flex
# Reading package lists...
# Building dependency tree...
# Reading state information...
# dpkg-dev is already the newest version (1.20.13).
# Suggested packages:
#   bison build-essential flex-doc
# Recommended packages:
#   libfl-dev
# The following NEW packages will be installed:
#   flex
# 0 upgraded, 1 newly installed, 0 to remove and 0 not upgraded.
# Need to get 440 kB of archives.
# After this operation, 1310 kB of additional disk space will be used.
# Get:1 http://deb.debian.org/debian bullseye/main amd64 flex amd64 2.6.4-8 [440 kB]
# debconf: delaying package configuration, since apt-utils is not installed
# Fetched 440 kB in 36s (12.2 kB/s)
# Selecting previously unselected package flex.
# (Reading database ... 22793 files and directories currently installed.)
# Preparing to unpack .../flex_2.6.4-8_amd64.deb ...
# Unpacking flex (2.6.4-8) ...
# Setting up flex (2.6.4-8) ...
# + rm -r /var/lib/apt/lists/auxfiles /var/lib/apt/lists/deb.debian.org_debian-security_dists_bullseye-security_InRelease /var/lib/apt/lists/deb.debian.org_debian-security_dists_bullseye-security_main_binary-amd64_Packages.lz4 /var/lib/apt/lists/deb.debian.org_debian_dists_bullseye-updates_InRelease /var/lib/apt/lists/deb.debian.org_debian_dists_bullseye-updates_main_binary-amd64_Packages.lz4 /var/lib/apt/lists/deb.debian.org_debian_dists_bullseye_InRelease /var/lib/apt/lists/deb.debian.org_debian_dists_bullseye_main_binary-amd64_Packages.lz4 /var/lib/apt/lists/lock /var/lib/apt/lists/partial
# + _fetch gcc-12.2.0/gcc-12.2.0.tar.xz.sig gcc.tar.xz.sig
# + local fetch=gcc-12.2.0/gcc-12.2.0.tar.xz.sig
# + shift
# + local file=gcc.tar.xz.sig
# + shift
# + curl -fL https://ftpmirror.gnu.org/gcc/gcc-12.2.0/gcc-12.2.0.tar.xz.sig -o gcc.tar.xz.sig
#   % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
#                                  Dload  Upload   Total   Spent    Left  Speed
#   0     0    0     0    0     0      0      0 --:--:--  0:00:01 --:--:--     0curl: (7) Couldn't connect to server
# + curl -fL https://mirrors.kernel.org/gnu/gcc/gcc-12.2.0/gcc-12.2.0.tar.xz.sig -o gcc.tar.xz.sig
#   % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
#                                  Dload  Upload   Total   Spent    Left  Speed
# 100   310  100   310    0     0    137      0  0:00:02  0:00:02 --:--:--   137
# + return 0
# + _fetch gcc-12.2.0/gcc-12.2.0.tar.xz gcc.tar.xz
# + local fetch=gcc-12.2.0/gcc-12.2.0.tar.xz
# + shift
# + local file=gcc.tar.xz
# + shift
# + curl -fL https://ftpmirror.gnu.org/gcc/gcc-12.2.0/gcc-12.2.0.tar.xz -o gcc.tar.xz
#   % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
#                                  Dload  Upload   Total   Spent    Left  Speed
#   0     0    0     0    0     0      0      0 --:--:--  0:00:01 --:--:--     0
# 100 80.7M  100 80.7M    0     0  1130k      0  0:01:13  0:01:13 --:--:-- 1161k
# + return 0
# + gpg --batch --verify gcc.tar.xz.sig gcc.tar.xz
# gpg: Signature made Fri Aug 19 08:38:41 2022 UTC
# gpg:                using RSA key 7F74F97C103468EE5D750B583AB00996FC26A641
# gpg: Good signature from "Richard Guenther <richard.guenther@gmail.com>" [unknown]
# gpg:                 aka "Richard Guenther (Work) <rguenther@suse.de>" [unknown]
# gpg:                 aka "Richard Guenther <richard.guenther@gmx.net>" [unknown]
# gpg:                 aka "Richard Guenther (GCC) <rguenth@gcc.gnu.org>" [unknown]
# gpg: WARNING: This key is not certified with a trusted signature!
# gpg:          There is no indication that the signature belongs to the owner.
# Primary key fingerprint: 1397 5A70 E63C 361C 73AE  69EF 6EEB 81F8 981C 74C7
#      Subkey fingerprint: 7F74 F97C 1034 68EE 5D75  0B58 3AB0 0996 FC26 A641
# + mkdir -p /usr/src/gcc
# + tar -xf gcc.tar.xz -C /usr/src/gcc --strip-components=1
# + rm gcc.tar.xz gcc.tar.xz.sig
# + cd /usr/src/gcc
# + ./contrib/download_prerequisites
# # 2023-11-04 02:24:11 URL:http://gcc.gnu.org/pub/gcc/infrastructure/gmp-6.2.1.tar.bz2 [2493916/2493916] -> "gmp-6.2.1.tar.bz2" [1]
# # 2023-11-04 02:25:32 URL:http://gcc.gnu.org/pub/gcc/infrastructure/mpfr-4.1.0.tar.bz2 [1747243/1747243] -> "mpfr-4.1.0.tar.bz2" [1]
# # 2023-11-04 02:27:44 URL:http://gcc.gnu.org/pub/gcc/infrastructure/mpc-1.2.1.tar.gz [838731/838731] -> "mpc-1.2.1.tar.gz" [1]
# # 2023-11-04 02:29:24 URL:http://gcc.gnu.org/pub/gcc/infrastructure/isl-0.24.tar.bz2 [2261594/2261594] -> "isl-0.24.tar.bz2" [1]
# gmp-6.2.1.tar.bz2: OK
# mpfr-4.1.0.tar.bz2: OK
# mpc-1.2.1.tar.gz: OK
# isl-0.24.tar.bz2: OK
# All prerequisites downloaded successfully.
# + rm gmp-6.2.1.tar.bz2 isl-0.24.tar.bz2 mpc-1.2.1.tar.gz mpfr-4.1.0.tar.bz2
# + wget -O config.guess https://git.savannah.gnu.org/cgit/config.git/plain/config.guess?id=7d3d27baf8107b630586c962c057e22149653deb
# --2023-11-04 02:29:27--  https://git.savannah.gnu.org/cgit/config.git/plain/config.guess?id=7d3d27baf8107b630586c962c057e22149653deb
# Resolving git.savannah.gnu.org (git.savannah.gnu.org)... 209.51.188.168, 2001:470:142::168
# Connecting to git.savannah.gnu.org (git.savannah.gnu.org)|209.51.188.168|:443... connected.
# HTTP request sent, awaiting response... 200 OK
# Length: 44259 (43K) [text/plain]
# Saving to: 'config.guess'

#      0K .......... .......... .......... .......... ...       100%  129K=0.3s

# 2023-11-04 02:29:29 (129 KB/s) - 'config.guess' saved [44259/44259]

# + find -mindepth 2 -name config.guess -exec cp -v config.guess {} ;
# 'config.guess' -> './gmp-6.2.1/config.guess'
# 'config.guess' -> './mpfr-4.1.0/config.guess'
# 'config.guess' -> './mpc-1.2.1/build-aux/config.guess'
# 'config.guess' -> './isl-0.24/interface/config.guess'
# 'config.guess' -> './isl-0.24/config.guess'

# + wget -O config.sub https://git.savannah.gnu.org/cgit/config.git/plain/config.sub?id=7d3d27baf8107b630586c962c057e22149653deb
# --2023-11-04 02:29:29--  https://git.savannah.gnu.org/cgit/config.git/plain/config.sub?id=7d3d27baf8107b630586c962c057e22149653deb
# Resolving git.savannah.gnu.org (git.savannah.gnu.org)... 209.51.188.168, 2001:470:142::168
# Connecting to git.savannah.gnu.org (git.savannah.gnu.org)|209.51.188.168|:443... connected.
# HTTP request sent, awaiting response... 200 OK
# Length: 36515 (36K) [text/plain]
# Saving to: 'config.sub'

#      0K .......... .......... .......... .....                100% 52.4K=0.7s

# 2023-11-04 02:29:32 (52.4 KB/s) - 'config.sub' saved [36515/36515]

# + find -mindepth 2 -name config.sub -exec cp -v config.sub {} ;
# 'config.sub' -> './gmp-6.2.1/config.sub'
# 'config.sub' -> './mpfr-4.1.0/config.sub'
# 'config.sub' -> './mpc-1.2.1/build-aux/config.sub'
# 'config.sub' -> './isl-0.24/interface/config.sub'
# 'config.sub' -> './isl-0.24/config.sub'
# + mktemp -d
# + dir=/tmp/tmp.ydk4pOBEpM
# + cd /tmp/tmp.ydk4pOBEpM
# + extraConfigureArgs=
# + dpkg --print-architecture
# + dpkgArch=amd64
# + dpkg-architecture --query DEB_BUILD_GNU_TYPE
# + gnuArch=x86_64-linux-gnu
# + /usr/src/gcc/configure --build=x86_64-linux-gnu --disable-multilib --enable-languages=c,c++,fortran,go
# + nproc
# + make -j 16
# + make install-strip
# + cd ..
# + rm -rf /tmp/tmp.ydk4pOBEpM /usr/src/gcc
# + apt-mark auto .*
# + [ -z autoconf
# automake
# bzip2
# ca-certificates
# curl
# default-libmysqlclient-dev
# dpkg-dev
# file
# g++
# gcc
# git
# gnupg
# imagemagick
# libbz2-dev
# libc6-dev
# libcurl4-openssl-dev
# libdb-dev
# libevent-dev
# libffi-dev
# libgdbm-dev
# libglib2.0-dev
# libgmp-dev
# libjpeg-dev
# libkrb5-dev
# liblzma-dev
# libmagickcore-dev
# libmagickwand-dev
# libmaxminddb-dev
# libncurses5-dev
# libncursesw5-dev
# libpng-dev
# libpq-dev
# libreadline-dev
# libsqlite3-dev
# libssl-dev
# libtool
# libwebp-dev
# libxml2-dev
# libxslt1-dev
# libyaml-dev
# make
# mercurial
# netbase
# openssh-client
# patch
# procps
# subversion
# unzip
# wget
# xz-utils
# zlib1g-dev ]
# + apt-mark manual autoconf automake bzip2 ca-certificates curl default-libmysqlclient-dev dpkg-dev file g++ gcc git gnupg imagemagick libbz2-dev libc6-dev libcurl4-openssl-dev libdb-dev libevent-dev libffi-dev libgdbm-dev libglib2.0-dev libgmp-dev libjpeg-dev libkrb5-dev liblzma-dev libmagickcore-dev libmagickwand-dev libmaxminddb-dev libncurses5-dev libncursesw5-dev libpng-dev libpq-dev libreadline-dev libsqlite3-dev libssl-dev libtool libwebp-dev libxml2-dev libxslt1-dev libyaml-dev make mercurial netbase openssh-client patch procps subversion unzip wget xz-utils zlib1g-dev
# + apt-get purge -y --auto-remove -o APT::AutoRemove::RecommendsImportant=false


# gcc installs .so files in /usr/local/lib64 (and /usr/local/lib)...
RUN set -ex; \
# this filename needs to sort higher than all the architecture filenames ("aarch64-...", "armeabi...", etc)
	{ echo '/usr/local/lib64'; echo '/usr/local/lib'; } > /etc/ld.so.conf.d/000-local-lib.conf; \
	ldconfig -v
# Step 8/9 : RUN
# set -ex;
# { echo '/usr/local/lib64'; echo '/usr/local/lib'; } > /etc/ld.so.conf.d/000-local-lib.conf;
# ldconfig -v

# ensure that alternatives are pointing to the new compiler and that old one is no longer used
RUN set -ex; \
	dpkg-divert --divert /usr/bin/gcc.orig --rename /usr/bin/gcc; \
	dpkg-divert --divert /usr/bin/g++.orig --rename /usr/bin/g++; \
	dpkg-divert --divert /usr/bin/gfortran.orig --rename /usr/bin/gfortran; \
	update-alternatives --install /usr/bin/cc cc /usr/local/bin/gcc 999
# Step 9/9 : RUN
# set -ex;
# dpkg-divert --divert /usr/bin/gcc.orig --rename /usr/bin/gcc;
# dpkg-divert --divert /usr/bin/g++.orig --rename /usr/bin/g++;
# dpkg-divert --divert /usr/bin/gfortran.orig --rename /usr/bin/gfortran;
# update-alternatives --install /usr/bin/cc cc /usr/local/bin/gcc 999
