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
# https://flutter.dev/docs/get-started/install/linux
RUN apt -y install curl
RUN apt -y install file
RUN apt -y install unzip
RUN apt -y install xz-utils
RUN apt -y install zip

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