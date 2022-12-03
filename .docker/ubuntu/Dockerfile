FROM dorowu/ubuntu-desktop-lxde-vnc:latest
WORKDIR /usr/local/

RUN wget -q -O - https://dl.google.com/linux/linux_signing_key.pub | sudo apt-key add - 

RUN apt update
ARG FLUTTER_VERSION=stable

# Vim インストール
RUN apt -y install vim

# Gitインストール
RUN add-apt-repository ppa:git-core/ppa
RUN apt -y install git
RUN apt update

# flutter インストール
RUN git clone -b ${FLUTTER_VERSION} https://github.com/flutter/flutter
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
RUN apt -y install curl \
    file \
    unzip \
    xz-utils \
    zip

# Flutter Linux Desktop Setup
# https://docs.flutter.dev/get-started/install/linux#linux-setup
RUN apt -y install clang cmake ninja-build pkg-config libgtk-3-dev liblzma-dev

# Google Chromeインストール
RUN apt-get install google-chrome-stable

# Google Chrome Root実行用に書き換え
# https://askubuntu.com/questions/451290/how-to-run-chromium-as-root
RUN cp /usr/bin/google-chrome /usr/bin/google-chrome.bk
RUN sed -e '$d' /usr/bin/google-chrome >> /usr/bin/google-chrome.temp
RUN sed -e '$a exec -a "$0" "$HERE/chrome" "$@" --no-sandbox' /usr/bin/google-chrome.temp > /usr/bin/google-chrome
RUN rm -f /usr/bin/google-chrome.temp

# Flutter 設定
RUN flutter config —-enable-web
RUN flutter config --enable-linux-desktop