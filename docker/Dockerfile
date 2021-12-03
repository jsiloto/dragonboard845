FROM ubuntu:20.04


RUN : \
    && apt-get update \
    && DEBIAN_FRONTEND=noninteractive apt-get install -y --no-install-recommends \
        software-properties-common \
    && add-apt-repository -y ppa:deadsnakes \
    && DEBIAN_FRONTEND=noninteractive apt-get install -y --no-install-recommends \
        python3.8-venv \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/* \
    && :

RUN python3.8 -m venv /venv
ENV PATH=/venv/bin:$PATH

RUN apt-get update && apt-get install -y dirmngr gpg curl git rsync libncurses5 zip unzip

RUN git config --global user.email "you@example.com" &&  git config --global user.name "Your Name"

RUN REPO=$(mktemp /tmp/repo.XXXXXXXXX) && \
    curl -o ${REPO} https://storage.googleapis.com/git-repo-downloads/repo && \
    gpg --recv-key 8BB9AD793E8E6153AF0F9A4416530D5E920F5C65 && \
    curl -s https://storage.googleapis.com/git-repo-downloads/repo.asc | gpg --verify - ${REPO} && install -m 755 ${REPO} /bin/repo


RUN mkdir /home/user
WORKDIR /home/user

#RUN yes | repo init --depth=1 -u https://android.googlesource.com/platform/manifest -b master

#RUN repo sync  -c --no-clone-bundle --no-tags
