FROM debian:bullseye-slim

ENV LANG=C.UTF-8 LC_ALL=C.UTF-8
ENV PATH /opt/conda/bin:$PATH

# hadolint ignore=DL3008

RUN set -x && \
    apt-get update --fix-missing && \
    apt-get install -y --no-install-recommends \
        bzip2 \
        ca-certificates \
        git \
        libglib2.0-0 \
        libsm6 \
        libxcomposite1 \
        libxcursor1 \
        libxdamage1 \
        libxext6 \
        libxfixes3 \
        libxi6 \
        libxinerama1 \
        libxrandr2 \
        libxrender1 \
        mercurial \
        openssh-client \
        procps \
        subversion \
        wget \
        curl \
	    tmux && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/* && \
    UNAME_M="$(uname -m)" && \
    ANACONDA_BASE="https://repo.anaconda.com/archive" && \
    ANACONDA_VERSION="$(curl -sL https://repo.anaconda.com/archive |grep ".*Anaconda3-.*-Linux" | head -1 | cut -d"-" -f 2,3)" && \
    ANACONDA_URL=${ANACONDA_BASE}/Anaconda3-${ANACONDA_VERSION}-Linux-${UNAME_M}.sh && \
    SHA256SUM=$(curl -sL ${ANACONDA_BASE} | grep -A 3 Anaconda3-${ANACONDA_VERSION}-Linux-${UNAME_M}.sh |cut -d">" -f 2 |cut -d"<" -f 1 | tail -1) && \
    wget "${ANACONDA_URL}" -O anaconda.sh -q && \
    echo "${SHA256SUM}  anaconda.sh" > shasum && \
    sha256sum --check --status shasum && \
    /bin/bash anaconda.sh -b -p /opt/conda && \
    rm anaconda.sh shasum && \
    ln -s /opt/conda/etc/profile.d/conda.sh /etc/profile.d/conda.sh && \
    echo ". /opt/conda/etc/profile.d/conda.sh" >> ~/.bashrc && \
    echo "conda activate base" >> ~/.bashrc && \
    find /opt/conda/ -follow -type f -name '*.a' -delete && \
    find /opt/conda/ -follow -type f -name '*.js.map' -delete && \
    /opt/conda/bin/conda clean -afy

LABEL software="Anaconda TMUX" \ 
	base_image="debian:bullseye-slim" \ 
	container="anacondatmux" \
	about.summary="Docker container with latest anaconda distribution and tmux terminal multiplexer" \ 
	software.version="2023.09-0" \
	version="1.0"

CMD [ "/bin/bash" ]
