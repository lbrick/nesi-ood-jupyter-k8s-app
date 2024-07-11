FROM ubuntu:22.04

# run unminimise, e.g. for man pages to work
RUN yes | unminimize

# install system dependencies
# TODO: move ldap-utils, libnss-ldapd, libpam-ldapd, nscd, nslcd to base image??
RUN apt-get update && DEBIAN_FRONTEND=noninteractive apt-get install -y \
        curl \
        git \
        ldap-utils \
        libnss-ldapd \
        libpam-ldapd \
        less \
        nano \
        nodejs \
        nscd \
        nslcd \
        python-is-python3 \
        python3 \
        python3-pip \
        rsync \
        unzip \
        vim \
        wget \
        zip \
    && rm -rf /var/lib/apt/lists/*

# install nodejs 20
ADD https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.7/install.sh /tmp/install-1.sh
RUN bash /tmp/install-1.sh \
    && export NVM_DIR="$HOME/.nvm" \
    && . "$NVM_DIR/nvm.sh" \
    && nvm install 20
RUN node -v

# install lmod
RUN apt-get update && DEBIAN_FRONTEND=noninteractive apt-get install -y \
        lua5.3 \
        lua-bit32:amd64 \
        lua-posix:amd64 \
        lua-posix-dev \
        liblua5.3-0:amd64 \
        liblua5.3-dev:amd64 \
        tcl \
        tcl-dev \
        tcl8.6 \
        tcl8.6-dev:amd64 \
        libtcl8.6:amd64
RUN wget https://sourceforge.net/projects/lmod/files/Lmod-8.7.tar.bz2 \
    && tar -xjvf Lmod-8.7.tar.bz2
WORKDIR /Lmod-8.7
RUN ./configure --prefix=/opt/apps \
    && make install \
    && ln -s /opt/apps/lmod/lmod/init/profile /etc/profile.d/z00_lmod.sh \
    && ln -s /opt/apps/lmod/lmod/init/cshrc /etc/profile.d/z00_lmod.csh

# clean up
RUN rm -f /Lmod-8.7.tar.bz2
WORKDIR /

# install jupyterlab
RUN pip3 --no-cache-dir install jupyterlab jupyterlmod