# Docker Flutter環境

# Requirement
* [docker](https://www.docker.com/)

# Install
`.env.example` をコピー `.env` を作成。
各種設定値を修正。

Docker起動
```
cd .docker
docker-compose up -d --build
```

コンテナに入る
```
docker exec -it flutter bash
```

# Usage

## flutter の状況確認
`flutter doctor`


## 作業フォルダ
`./src`

## リモートデスクトップに接続
http://127.0.0.1:6080/

# Sample
1. 作業ディレクトリ
```
cd /src
```

2. サンプル作成
flutter サンプルを作成
```
flutter create .
```

3. サンプル起動
port:55555 でサーバー起動
```
flutter run -d web-server --web-port 55555 --web-hostname 0.0.0.0
```
http://localhost:55555 で確認


or

Linuxデスクトップで確認

リモートデスクトップに接続
http://127.0.0.1:6080/

コンソール上で以下のコマンド
```
cd /flutter/
flutter run -d
```

4. build
```
flutter build web
```

## Android Studio設定

1. Androidの設定
以下の設定を有効にするとAndoroid Studioをインストールします。
`.env.example` → `.env`
`INSTALL_ANDROID=true`

2. Andoroid Studioの起動
Docker build後にDocker内（ http://127.0.0.1:6080/ ）で実行して `Andoroid Studio` を設定してください。
`/opt/android-studio/bin/studio.sh`

3. Andoroid Studioの設定
起動後
ダイアログの右下のConfigure > Android SDK > タブのSDK Toolsを選択 > Android ADK Command-line Tools をチェック > OK

※初期起動のダイアログでやり忘れたら以下の手順で実行
Andoroid Studio 起動中
ツールバー Tools > SDK Toolsを選択 > Android ADK Command-line Tools をチェック > OK

4. SDKの設定
```
flutter config --android-sdk /root/Android/Sdk
```

`/root/Andorid/Sdk` を適宜変えてください。

4. Androidの設定
```
flutter doctor --android-licenses
```

全て `y` で OK です。

5. インストールの確認
```
flutter doctor
```

# Note
* [Android Studio のインストール](https://developer.android.com/studio/install?hl=ja)
* [How to install Android Studio on Ubuntu 20.04](https://vitux.com/how-to-install-android-studio-on-ubuntu-20-04/)
* [Flutter Linux setup](https://flutter.dev/docs/get-started/install/linux#linux-setup)
* [dorowu/ubuntu-desktop-lxde-vnc](https://hub.docker.com/r/dorowu/ubuntu-desktop-lxde-vnc/) 

# Author
* [こぴぺたん](https://twitter.com/c_a_p_engineer)

# License
[MIT license](https://en.wikipedia.org/wiki/MIT_License).
