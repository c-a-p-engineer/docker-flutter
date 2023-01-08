FROM dorowu/ubuntu-desktop-lxde-vnc:latest
WORKDIR /usr/local/

RUN wget -q -O - https://dl.google.com/linux/linux_signing_key.pub | sudo apt-key add - 

# パッケージ取得先を変更
RUN sed -i 's@archive.ubuntu.com@ftp.jaist.ac.jp/pub/Linux@g' /etc/apt/sources.list

ARG FLUTTER_VERSION=stable

# Git Vim インストール
RUN add-apt-repository ppa:git-core/ppa
RUN apt-get update && apt-get install -y \
    git \
    vim \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*

# flutter インストール
RUN git clone --depth=1 -b ${FLUTTER_VERSION} https://github.com/flutter/flutter
ENV PATH $PATH:PATH:/usr/local/flutter/bin

ARG INSTALL_ANDROID=false
RUN if [ ${INSTALL_ANDROID} = true ]; then \
    # Java インストール
    apt -y install openjdk-11-jdk;\
    export JAVA_HOME="/usr/lib/jvm/java-1.11.0-openjdk-amd64"; \
    # Android Studioインストール
    add-apt-repository ppa:maarten-fonville/android-studio; \
    apt -y install android-studio; \
    apt update; \
fi

# Flutter ビルド用パッケージのインストール
# https://flutter.dev/docs/get-started/install/linux
RUN apt-get update && apt -y install \
    curl \
    file \
    unzip \
    xz-utils \
    zip \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*

# Flutter Linux Desktop Setup
# https://docs.flutter.dev/get-started/install/linux#linux-setup
RUN apt-get update && apt -y install \
    clang \
    cmake \
    ninja-build \
    pkg-config \
    libgtk-3-dev \
    liblzma-dev \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*

# Google Chromeインストール
RUN curl -O https://packages.cloud.google.com/apt/doc/apt-key.gpg && apt-key add apt-key.gpg
RUN apt-get update && apt -y install \
    google-chrome-stable \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*

# Google Chrome Root実行用に書き換え
# https://askubuntu.com/questions/451290/how-to-run-chromium-as-root
RUN cp /usr/bin/google-chrome /usr/bin/google-chrome.bk
RUN sed -e '$d' /usr/bin/google-chrome >> /usr/bin/google-chrome.temp
RUN sed -e '$a exec -a "$0" "$HERE/chrome" "$@" --no-sandbox' /usr/bin/google-chrome.temp > /usr/bin/google-chrome
RUN rm -f /usr/bin/google-chrome.temp

# Flutter 設定
RUN flutter config —-enable-web
RUN flutter config --enable-linux-desktop
