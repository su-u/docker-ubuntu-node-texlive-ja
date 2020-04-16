FROM su1101/ubuntu-node

# PATH
ENV TEXLIVE_PATH /usr/local/texlive
ENV FONT_PATH ${TEXLIVE_PATH}/texmf-local/fonts
ENV PATH $TEXLIVE_PATH/bin/x86_64-linuxmusl:/bin:$PATH

RUN apt-get update && \
    # Install basic dependencies
    apt-get install -y wget make perl ghostscript bash git ca-certificates && \
    # Install TeXLive
    apt-get install -y \
    tar \ 
    gnupg \
    perl-modules-5.28 \
    fontconfig \
    musl-dev && \
    mkdir /tmp/install-tl-unx && \
    wget -qO- http://mirror.ctan.org/systems/texlive/tlnet/install-tl-unx.tar.gz | \
    tar -xz -C /tmp/install-tl-unx --strip-components=1 && \
    printf "%s\n" \
      "TEXDIR $TEXLIVE_PATH" \
      "selected_scheme scheme-basic" \
      "option_doc 0" \
      "option_src 0" \
      > /tmp/install-tl-unx/texlive.profile && \
    /tmp/install-tl-unx/install-tl -profile /tmp/install-tl-unx/texlive.profile && \
    tlmgr install collection-latexextra collection-langjapanese collection-fontsrecommended && \
    rm -rf /tmp/install-tl-unx && \
    # Install llmk
    wget -qO /usr/local/bin/llmk https://raw.githubusercontent.com/wtsnjp/llmk/master/llmk.lua && \
    chmod +x /usr/local/bin/llmk && \
    # Install and apply fonts
    git clone https://github.com/trueroad/HaranoAjiFonts.git && \
    mkdir -p "${FONT_PATH}/opentype/haranoaji" && \
    cp -p ./HaranoAjiFonts/*.otf "${FONT_PATH}/opentype/haranoaji/" && \
    rm -rf ./HaranoAjiFonts && \
    mktexlsr && \
    rm -rf /var/cache/apt/archives/* /var/lib/apt/lists/*

WORKDIR /workdir

VOLUME ["/workdir"]

CMD ["bash"]