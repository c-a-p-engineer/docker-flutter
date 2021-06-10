FROM dorowu/ubuntu-desktop-lxde-vnc
WORKDIR /usr/local/
RUN apt update

# Vim インストール
RUN apt -y install vim

# Gitインストール
RUN add-apt-repository ppa:git-core/ppa
RUN apt -y install git
RUN apt update

# flutter インストール
RUN git clone -b stable https://github.com/flutter/flutter
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
# https://qiita.com/kurun_pan/items/47c25a4b2425725bc199#%E3%83%93%E3%83%AB%E3%83%89%E3%81%A7%E5%BF%85%E8%A6%81%E3%81%AB%E3%81%AA%E3%82%8B%E3%83%91%E3%83%83%E3%82%B1%E3%83%BC%E3%82%B8%E3%81%AE%E3%82%A4%E3%83%B3%E3%82%B9%E3%83%88%E3%83%BC%E3%83%AB
RUN apt -y install clang curl pkg-config ninja-build cmake libgtk-3-dev libblkid-dev liblzma-dev unzip

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