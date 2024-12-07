#
# NOTE: THIS DOCKERFILE IS GENERATED VIA "apply-templates.sh"
#
# PLEASE DO NOT EDIT IT DIRECTLY.
#

FROM buildpack-deps:bullseye-scm
# Step 1/2 : FROM buildpack-deps:bullseye-scm

RUN set -ex; \
	apt-get update; \
	apt-get install -y --no-install-recommends \
		autoconf \
		automake \
		bzip2 \
		dpkg-dev \
		file \
		g++ \
		gcc \
		imagemagick \
		libbz2-dev \
		libc6-dev \
		libcurl4-openssl-dev \
		libdb-dev \
		libevent-dev \
		libffi-dev \
		libgdbm-dev \
		libglib2.0-dev \
		libgmp-dev \
		libjpeg-dev \
		libkrb5-dev \
		liblzma-dev \
		libmagickcore-dev \
		libmagickwand-dev \
		libmaxminddb-dev \
		libncurses5-dev \
		libncursesw5-dev \
		libpng-dev \
		libpq-dev \
		libreadline-dev \
		libsqlite3-dev \
		libssl-dev \
		libtool \
		libwebp-dev \
		libxml2-dev \
		libxslt-dev \
		libyaml-dev \
		make \
		patch \
		unzip \
		xz-utils \
		zlib1g-dev \
		\
# https://lists.debian.org/debian-devel-announce/2016/09/msg00000.html
		$( \
# if we use just "apt-cache show" here, it returns zero because "Can't select versions from package 'libmysqlclient-dev' as it is purely virtual", hence the pipe to grep
			if apt-cache show 'default-libmysqlclient-dev' 2>/dev/null | grep -q '^Version:'; then \
				echo 'default-libmysqlclient-dev'; \
			else \
				echo 'libmysqlclient-dev'; \
			fi \
		) \
	; \
	rm -rf /var/lib/apt/lists/*

# Step 2/2 : RUN
# set -ex;
# apt-get update;
# apt-get install -y --no-install-recommends autoconf automake bzip2 dpkg-dev file g++ gcc imagemagick libbz2-dev libc6-dev libcurl4-openssl-dev libdb-dev libevent-dev libffi-dev libgdbm-dev libglib2.0-dev libgmp-dev libjpeg-dev libkrb5-dev liblzma-dev libmagickcore-dev libmagickwand-dev libmaxminddb-dev libncurses5-dev libncursesw5-dev libpng-dev libpq-dev libreadline-dev libsqlite3-dev libssl-dev libtool libwebp-dev libxml2-dev libxslt-dev libyaml-dev make patch unzip xz-utils zlib1g-dev $(if apt-cache show 'default-libmysqlclient-dev' 2>/dev/null | grep -q '^Version:'; then echo 'default-libmysqlclient-dev'; else echo 'libmysqlclient-dev'; fi);
# rm -rf /var/lib/apt/lists/*

# The following additional packages will be installed:
#   autotools-dev binutils binutils-common binutils-x86-64-linux-gnu comerr-dev
#   cpp cpp-10 fontconfig fontconfig-config fonts-dejavu-core g++-10 gcc-10
#   gir1.2-freedesktop gir1.2-gdkpixbuf-2.0 gir1.2-glib-2.0 gir1.2-rsvg-2.0
#   hicolor-icon-theme icu-devtools imagemagick-6-common imagemagick-6.q16
#   krb5-multidev libaom0 libasan6 libatomic1 libbinutils libblkid-dev
#   libbrotli-dev libc-dev-bin libcairo-gobject2 libcairo-script-interpreter2
#   libcairo2 libcairo2-dev libcc1-0 libcrypt-dev libctf-nobfd0 libctf0
#   libdatrie1 libdav1d4 libdb5.3-dev libde265-0 libdeflate-dev libdeflate0
#   libdjvulibre-dev libdjvulibre-text libdjvulibre21 libdpkg-perl libelf1
#   libevent-2.1-7 libevent-core-2.1-7 libevent-extra-2.1-7
#   libevent-openssl-2.1-7 libevent-pthreads-2.1-7 libexif-dev libexif12
#   libexpat1-dev libfftw3-double3 libfontconfig-dev libfontconfig1
#   libfontconfig1-dev libfreetype-dev libfreetype6 libfreetype6-dev libfribidi0
#   libgcc-10-dev libgdk-pixbuf-2.0-0 libgdk-pixbuf-2.0-dev libgdk-pixbuf2.0-bin
#   libgdk-pixbuf2.0-common libgirepository-1.0-1 libglib2.0-0 libglib2.0-bin
#   libglib2.0-data libglib2.0-dev-bin libgmpxx4ldbl libgomp1 libgraphite2-3
#   libgssrpc4 libharfbuzz0b libheif1 libice-dev libice6 libicu-dev libicu67
#   libilmbase-dev libilmbase25 libisl23 libitm1 libjbig-dev libjbig0
#   libjpeg62-turbo libjpeg62-turbo-dev libkadm5clnt-mit12 libkadm5srv-mit12
#   libkdb5-10 liblcms2-2 liblcms2-dev liblqr-1-0 liblqr-1-0-dev liblsan0
#   libltdl-dev libltdl7 liblzo2-2 libmagic-mgc libmagic1
#   libmagickcore-6-arch-config libmagickcore-6-headers libmagickcore-6.q16-6
#   libmagickcore-6.q16-6-extra libmagickcore-6.q16-dev libmagickwand-6-headers
#   libmagickwand-6.q16-6 libmagickwand-6.q16-dev libmariadb-dev
#   libmariadb-dev-compat libmariadb3 libmaxminddb0 libmount-dev libmpc3
#   libmpfr6 libncurses-dev libnsl-dev libnuma1 libopenexr-dev libopenexr25
#   libopenjp2-7 libopenjp2-7-dev libpango-1.0-0 libpangocairo-1.0-0
#   libpangoft2-1.0-0 libpcre16-3 libpcre2-16-0 libpcre2-32-0 libpcre2-dev
#   libpcre2-posix2 libpcre3-dev libpcre32-3 libpcrecpp0v5 libpixman-1-0
#   libpixman-1-dev libpng16-16 libpq5 libpthread-stubs0-dev libquadmath0
#   librsvg2-2 librsvg2-common librsvg2-dev libselinux1-dev libsepol1-dev
#   libsigsegv2 libsm-dev libsm6 libstdc++-10-dev libthai-data libthai0
#   libtiff-dev libtiff5 libtiffxx5 libtirpc-dev libtsan0 libubsan1 libwebp6
#   libwebpdemux2 libwebpmux3 libwmf-dev libwmf0.2-7 libx11-6 libx11-data
#   libx11-dev libx265-192 libxau-dev libxau6 libxcb-render0 libxcb-render0-dev
#   libxcb-shm0 libxcb-shm0-dev libxcb1 libxcb1-dev libxdmcp-dev libxdmcp6
#   libxext-dev libxext6 libxml2 libxrender-dev libxrender1 libxslt1.1 libxt-dev
#   libxt6 libyaml-0-2 linux-libc-dev m4 mariadb-common mysql-common pkg-config
#   python3-distutils python3-lib2to3 shared-mime-info uuid-dev x11-common
#   x11proto-dev x11proto-xext-dev xorg-sgml-doctools xtrans-dev
# Suggested packages:
#   autoconf-archive gnu-standards autoconf-doc gettext binutils-doc bzip2-doc
#   doc-base cpp-doc gcc-10-locales debian-keyring g++-multilib g++-10-multilib
#   gcc-10-doc gcc-multilib manpages-dev flex bison gdb gcc-doc gcc-10-multilib
#   imagemagick-doc autotrace cups-bsd | lpr | lprng enscript ffmpeg gimp
#   gnuplot grads graphviz groff-base hp2xx html2ps libwmf-bin mplayer povray
#   radiance sane-utils texlive-base-bin transfig ufraw-batch xdg-utils krb5-doc
#   glibc-doc libcairo2-doc libcurl4-doc libidn11-dev libldap2-dev librtmp-dev
#   libssh2-1-dev db5.3-doc bzr libfftw3-bin libfftw3-dev freetype2-doc
#   libgirepository1.0-dev libglib2.0-doc libxml2-utils gmp-doc libgmp10-doc
#   libmpfr-dev krb5-user libice-doc icu-doc liblcms2-utils libtool-doc
#   liblzma-doc inkscape mmdb-bin ncurses-doc postgresql-doc-13 readline-doc
#   librsvg2-bin librsvg2-doc libsm-doc sqlite3-doc libssl-doc libstdc++-10-doc
#   gfortran | fortran95-compiler gcj-jdk libwmf-doc libwmf0.2-7-gtk libx11-doc
#   libxcb-doc libxext-doc libxt-doc libyaml-doc m4-doc make-doc ed
#   diffutils-doc zip
# Recommended packages:
#   build-essential fakeroot libalgorithm-merge-perl ghostscript netpbm
#   bzip2-doc manpages manpages-dev libc-devtools libfile-fcntllock-perl
#   liblocale-gettext-perl libexif-doc xdg-user-dirs gsfonts libjxr-tools
#   libpng-tools
# The following NEW packages will be installed:
#   autoconf automake autotools-dev binutils binutils-common
#   binutils-x86-64-linux-gnu bzip2 comerr-dev cpp cpp-10
#   default-libmysqlclient-dev dpkg-dev file fontconfig fontconfig-config
#   fonts-dejavu-core g++ g++-10 gcc gcc-10 gir1.2-freedesktop
#   gir1.2-gdkpixbuf-2.0 gir1.2-glib-2.0 gir1.2-rsvg-2.0 hicolor-icon-theme
#   icu-devtools imagemagick imagemagick-6-common imagemagick-6.q16
#   krb5-multidev libaom0 libasan6 libatomic1 libbinutils libblkid-dev
#   libbrotli-dev libbz2-dev libc-dev-bin libc6-dev libcairo-gobject2
#   libcairo-script-interpreter2 libcairo2 libcairo2-dev libcc1-0 libcrypt-dev
#   libctf-nobfd0 libctf0 libcurl4-openssl-dev libdatrie1 libdav1d4 libdb-dev
#   libdb5.3-dev libde265-0 libdeflate-dev libdeflate0 libdjvulibre-dev
#   libdjvulibre-text libdjvulibre21 libdpkg-perl libelf1 libevent-2.1-7
#   libevent-core-2.1-7 libevent-dev libevent-extra-2.1-7 libevent-openssl-2.1-7
#   libevent-pthreads-2.1-7 libexif-dev libexif12 libexpat1-dev libffi-dev
#   libfftw3-double3 libfontconfig-dev libfontconfig1 libfontconfig1-dev
#   libfreetype-dev libfreetype6 libfreetype6-dev libfribidi0 libgcc-10-dev
#   libgdbm-dev libgdk-pixbuf-2.0-0 libgdk-pixbuf-2.0-dev libgdk-pixbuf2.0-bin
#   libgdk-pixbuf2.0-common libgirepository-1.0-1 libglib2.0-0 libglib2.0-bin
#   libglib2.0-data libglib2.0-dev libglib2.0-dev-bin libgmp-dev libgmpxx4ldbl
#   libgomp1 libgraphite2-3 libgssrpc4 libharfbuzz0b libheif1 libice-dev libice6
#   libicu-dev libicu67 libilmbase-dev libilmbase25 libisl23 libitm1 libjbig-dev
#   libjbig0 libjpeg-dev libjpeg62-turbo libjpeg62-turbo-dev libkadm5clnt-mit12
#   libkadm5srv-mit12 libkdb5-10 libkrb5-dev liblcms2-2 liblcms2-dev liblqr-1-0
#   liblqr-1-0-dev liblsan0 libltdl-dev libltdl7 liblzma-dev liblzo2-2
#   libmagic-mgc libmagic1 libmagickcore-6-arch-config libmagickcore-6-headers
#   libmagickcore-6.q16-6 libmagickcore-6.q16-6-extra libmagickcore-6.q16-dev
#   libmagickcore-dev libmagickwand-6-headers libmagickwand-6.q16-6
#   libmagickwand-6.q16-dev libmagickwand-dev libmariadb-dev
#   libmariadb-dev-compat libmariadb3 libmaxminddb-dev libmaxminddb0
#   libmount-dev libmpc3 libmpfr6 libncurses-dev libncurses5-dev
#   libncursesw5-dev libnsl-dev libnuma1 libopenexr-dev libopenexr25
#   libopenjp2-7 libopenjp2-7-dev libpango-1.0-0 libpangocairo-1.0-0
#   libpangoft2-1.0-0 libpcre16-3 libpcre2-16-0 libpcre2-32-0 libpcre2-dev
#   libpcre2-posix2 libpcre3-dev libpcre32-3 libpcrecpp0v5 libpixman-1-0
#   libpixman-1-dev libpng-dev libpng16-16 libpq-dev libpq5
#   libpthread-stubs0-dev libquadmath0 libreadline-dev librsvg2-2
#   librsvg2-common librsvg2-dev libselinux1-dev libsepol1-dev libsigsegv2
#   libsm-dev libsm6 libsqlite3-dev libssl-dev libstdc++-10-dev libthai-data
#   libthai0 libtiff-dev libtiff5 libtiffxx5 libtirpc-dev libtool libtsan0
#   libubsan1 libwebp-dev libwebp6 libwebpdemux2 libwebpmux3 libwmf-dev
#   libwmf0.2-7 libx11-6 libx11-data libx11-dev libx265-192 libxau-dev libxau6
#   libxcb-render0 libxcb-render0-dev libxcb-shm0 libxcb-shm0-dev libxcb1
#   libxcb1-dev libxdmcp-dev libxdmcp6 libxext-dev libxext6 libxml2 libxml2-dev
#   libxrender-dev libxrender1 libxslt1-dev libxslt1.1 libxt-dev libxt6
#   libyaml-0-2 libyaml-dev linux-libc-dev m4 make mariadb-common mysql-common
#   patch pkg-config python3-distutils python3-lib2to3 shared-mime-info unzip
#   uuid-dev x11-common x11proto-dev x11proto-xext-dev xorg-sgml-doctools
#   xtrans-dev xz-utils zlib1g-dev
# 0 upgraded, 243 newly installed, 0 to remove and 0 not upgraded.
