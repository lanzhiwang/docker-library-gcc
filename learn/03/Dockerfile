#
# NOTE: THIS DOCKERFILE IS GENERATED VIA "apply-templates.sh"
#
# PLEASE DO NOT EDIT IT DIRECTLY.
#

FROM buildpack-deps:bullseye-curl
# Step 1/2 : FROM buildpack-deps:bullseye-curl

# procps is very common in build systems, and is a reasonably small package
RUN apt-get update && apt-get install -y --no-install-recommends \
		git \
		mercurial \
		openssh-client \
		subversion \
		\
		procps \
	&& rm -rf /var/lib/apt/lists/*
# Step 2/2 : RUN
# apt-get update &&
# apt-get install -y --no-install-recommends git mercurial openssh-client subversion procps &&
# rm -rf /var/lib/apt/lists/*

# The following additional packages will be installed:
#   git-man libapr1 libaprutil1 libbsd0 libcbor0 libcurl3-gnutls libedit2
#   liberror-perl libexpat1 libfido2-1 libgdbm-compat4 libgdbm6 libmd0 libmpdec3
#   libncurses6 libperl5.32 libprocps8 libpython3-stdlib libpython3.9-minimal
#   libpython3.9-stdlib libserf-1-1 libsvn1 libutf8proc2 media-types
#   mercurial-common perl perl-modules-5.32 python3 python3-minimal python3.9
#   python3.9-minimal sensible-utils ucf
# Suggested packages:
#   gettext-base git-daemon-run | git-daemon-sysvinit git-doc git-el git-email
#   git-gui gitk gitweb git-cvs git-mediawiki git-svn gdbm-l10n kdiff3
#   | kdiff3-qt | kompare | meld | tkcvs | mgdiff qct python3-mysqldb
#   python3-openssl python3-pygments wish keychain libpam-ssh monkeysphere
#   ssh-askpass perl-doc libterm-readline-gnu-perl | libterm-readline-perl-perl
#   make libtap-harness-archive-perl python3-doc python3-tk python3-venv
#   python3.9-venv python3.9-doc binutils binfmt-support db5.3-util
#   libapache2-mod-svn patch subversion-tools
# Recommended packages:
#   patch less libgpm2 xauth psmisc
# The following NEW packages will be installed:
#   git git-man libapr1 libaprutil1 libbsd0 libcbor0 libcurl3-gnutls libedit2
#   liberror-perl libexpat1 libfido2-1 libgdbm-compat4 libgdbm6 libmd0 libmpdec3
#   libncurses6 libperl5.32 libprocps8 libpython3-stdlib libpython3.9-minimal
#   libpython3.9-stdlib libserf-1-1 libsvn1 libutf8proc2 media-types mercurial
#   mercurial-common openssh-client perl perl-modules-5.32 procps python3
#   python3-minimal python3.9 python3.9-minimal sensible-utils subversion ucf
# 0 upgraded, 38 newly installed, 0 to remove and 0 not upgraded.
