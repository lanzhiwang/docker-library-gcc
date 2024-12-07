#
# NOTE: THIS DOCKERFILE IS GENERATED VIA "apply-templates.sh"
#
# PLEASE DO NOT EDIT IT DIRECTLY.
#

FROM debian:bullseye
# [1/3] FROM docker.io/library/debian:bullseye

RUN set -eux; \
	apt-get update; \
	apt-get install -y --no-install-recommends \
		ca-certificates \
		curl \
		netbase \
		wget \
	; \
	rm -rf /var/lib/apt/lists/*
# Step 2/3 : RUN
# set -eux;
# apt-get update;
# apt-get install -y --no-install-recommends ca-certificates curl netbase wget ;
# rm -rf /var/lib/apt/lists/*

# + apt-get update

# + apt-get install -y --no-install-recommends ca-certificates curl netbase wget
# Reading package lists...
# Building dependency tree...
# Reading state information...
# The following additional packages will be installed:
#   libbrotli1 libcurl4 libldap-2.4-2 libnghttp2-14 libpsl5 librtmp1 libsasl2-2
#   libsasl2-modules-db libssh2-1 openssl
# Recommended packages:
#   libldap-common publicsuffix libsasl2-modules
# The following NEW packages will be installed:
#   ca-certificates curl libbrotli1 libcurl4 libldap-2.4-2 libnghttp2-14 libpsl5
#   librtmp1 libsasl2-2 libsasl2-modules-db libssh2-1 netbase openssl wget
# 0 upgraded, 14 newly installed, 0 to remove and 0 not upgraded.

RUN set -ex; \
	if ! command -v gpg > /dev/null; then \
		apt-get update; \
		apt-get install -y --no-install-recommends \
			gnupg \
			dirmngr \
		; \
		rm -rf /var/lib/apt/lists/*; \
	fi
# Step 3/3 : RUN
# set -ex;
# if ! command -v gpg > /dev/null; then
# 	apt-get update;
# 	apt-get install -y --no-install-recommends gnupg dirmngr;
# 	rm -rf /var/lib/apt/lists/*;
# fi

# + command -v gpg
# + apt-get update

# + apt-get install -y --no-install-recommends gnupg dirmngr
# Reading package lists...
# Building dependency tree...
# Reading state information...
# The following additional packages will be installed:
#   gnupg-l10n gnupg-utils gpg gpg-agent gpg-wks-client gpg-wks-server gpgconf
#   gpgsm libassuan0 libksba8 libncursesw6 libnpth0 libreadline8 libsqlite3-0
#   pinentry-curses readline-common
# Suggested packages:
#   dbus-user-session libpam-systemd pinentry-gnome3 tor parcimonie xloadimage
#   scdaemon pinentry-doc readline-doc
# Recommended packages:
#   libgpm2
# The following NEW packages will be installed:
#   dirmngr gnupg gnupg-l10n gnupg-utils gpg gpg-agent gpg-wks-client
#   gpg-wks-server gpgconf gpgsm libassuan0 libksba8 libncursesw6 libnpth0
#   libreadline8 libsqlite3-0 pinentry-curses readline-common
# 0 upgraded, 18 newly installed, 0 to remove and 0 not upgraded.
