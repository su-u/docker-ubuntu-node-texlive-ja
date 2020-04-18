#ubuntu-node-texlive-haranoaji:lastest
FROM su1101/ubuntu-node:latest

MAINTAINER Futa HIRAKOBA
ENV DEBIAN_FRONTEND=noninteractive

# PATH
ENV TEXLIVE_PATH /usr/local/texlive
ENV FONT_PATH ${TEXLIVE_PATH}/texmf-local/fonts

RUN apt-get update && \
    apt-get install -y \
    git \
    xdvik-ja \ 
    evince \
    texlive-lang-cjk \
    latexmk \
    language-pack-ja \
    wget \
    xzdec \
    texlive-latex-extra && \
    apt-get clean && \
    rm -rf /var/cache/apt/archives/* /var/lib/apt/lists/*

RUN tlmgr init-usertree
RUN kanji-config-updmap-sys ipaex

WORKDIR /tmp

RUN git clone https://github.com/trueroad/HaranoAjiFonts.git && \
    mkdir -p "${FONT_PATH}/opentype/haranoaji" && \
    cp -p ./HaranoAjiFonts/*.otf "${FONT_PATH}/opentype/haranoaji/" && \
    rm -rf ./HaranoAjiFonts && \
    mktexlsr

WORKDIR /workdir

VOLUME ["/workdir"]

CMD ["bash"]