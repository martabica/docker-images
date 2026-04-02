
FROM centos:centos7

# Install dependencies

RUN yum -y update && \
    yum -y install \
        curl \
        tar \
        gzip \
        bzip2 \
        unzip \
        which \
        libgomp \
        libX11 \
        libXext \
        libSM \
        libICE \
        libxcb \
        mesa-libGL \
    && yum clean all

# ---- Space Ranger ----

ARG SPACERANGER_URL

WORKDIR /opt

RUN curl -L "$SPACERANGER_URL" -o spaceranger.tar.gz && \
    tar -xzf spaceranger.tar.gz && \
    mv spaceranger-* spaceranger && \
    rm spaceranger.tar.gz

ENV PATH="/opt/spaceranger:$PATH"

WORKDIR /data

# Run spaceranger directly

ENTRYPOINT ["spaceranger"]
CMD ["--help"]
