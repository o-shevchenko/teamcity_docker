FROM jetbrains/teamcity-server:2018.1.2

RUN apt-get -q update \
    && apt-get -q install -y --no-install-recommends \
        apt-utils \
        build-essential \
        bzip2 \
        clang \
        curl \
        doxygen \
        fuse \
        g++ \
        gcc \
        git \
        gnupg-agent \
        libbz2-dev \
        libcurl4-openssl-dev \
        libfuse-dev \
        libprotobuf-dev \
        libprotoc-dev \
        libsasl2-dev \
        libsnappy-dev \
        libssl-dev \
        libtool \
        locales \
        make \
        pinentry-curses \
        pkg-config \
        python \
        python2.7 \
        python-pip \
        python-pkg-resources \
        python-setuptools \
        python-wheel \
        rsync \
        software-properties-common \
        snappy \
        sudo \
        valgrind \
        zlib1g-dev \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*
    
######
# Install cmake 3.1.0
######
RUN mkdir -p /opt/cmake \
    && curl -L -s -S \
      https://cmake.org/files/v3.1/cmake-3.1.0-Linux-x86_64.tar.gz \
      -o /opt/cmake.tar.gz \
    && tar xzf /opt/cmake.tar.gz --strip-components 1 -C /opt/cmake
ENV CMAKE_HOME /opt/cmake
ENV PATH "${PATH}:/opt/cmake/bin"

######
# Install Google Protobuf 2.5.0
######
# hadolint ignore=DL3003
RUN mkdir -p /opt/protobuf-src \
    && curl -L -s -S \
      https://github.com/google/protobuf/releases/download/v2.5.0/protobuf-2.5.0.tar.gz \
      -o /opt/protobuf.tar.gz \
    && tar xzf /opt/protobuf.tar.gz --strip-components 1 -C /opt/protobuf-src \
    && cd /opt/protobuf-src \
    && ./configure --prefix=/opt/protobuf \
    && make install \
    && cd /root \
    && rm -rf /opt/protobuf-src
ENV PROTOBUF_HOME /opt/protobuf
ENV PATH "${PATH}:/opt/protobuf/bin"

###
# Avoid out of memory errors in builds
###
ENV MAVEN_OPTS -Xms256m -Xmx1536m