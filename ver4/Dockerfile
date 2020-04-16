#ubuntu-node-texlive-llmk-haranoaji:lastest
FROM su1101/ubuntu-node:latest

MAINTAINER Futa HIRAKOBA
ENV DEBIAN_FRONTEND=noninteractive

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

# Set up fonts and llmk
RUN \
    # Run cjk-gs-integrate
      cjk-gs-integrate --cleanup --force && \
      cjk-gs-integrate --force && \
    # Copy CMap: 2004-{H,V}
      kanji-config-updmap-sys --jis2004 haranoaji && \
    # Re-index LuaTeX font database
      luaotfload-tool -u -f && \
    git clone https://github.com/trueroad/HaranoAjiFonts.git && \
    mkdir -p "${FONT_PATH}/opentype/haranoaji" && \
    cp -p ./HaranoAjiFonts/*.otf "${FONT_PATH}/opentype/haranoaji/" && \
    rm -rf ./HaranoAjiFonts && \
    mktexlsr && \
    # Install llmk
      wget -q -O /usr/local/bin/llmk https://raw.githubusercontent.com/wtsnjp/llmk/master/llmk.lua && \
      chmod +x /usr/local/bin/llmk

WORKDIR /workdir

VOLUME ["/workdir"]

CMD ["bash"]