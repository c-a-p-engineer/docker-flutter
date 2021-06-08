# Ubuntu Remote Desktop Docker環境

# Requirement
* [docker](https://www.docker.com/)

# Install
Docker起動
```
docker-compose up -d --build
```

コンテナに入る
```
docker exec -it flutter bash
```

## Android Studio起動
`/usr/local/android-studio/bin/studio.sh`

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
````

2.サンプル作成
flutter サンプルを作成
```
flutter create .
```

3.サンプル起動
port:55555 でサーバー起動
```
flutter run -d web-server --web-port 55555 --web-hostname 0.0.0.0
```
http://localhost:5555 で確認


4.build
```
flutter build web
```

# Note
* [Android Studio のインストール](https://developer.android.com/studio/install?hl=ja)
* [Flutter Linux setup](https://flutter.dev/docs/get-started/install/linux#linux-setup)
* [dorowu/ubuntu-desktop-lxde-vnc](https://hub.docker.com/r/dorowu/ubuntu-desktop-lxde-vnc/) 

# Author
* [こぴぺたん](https://twitter.com/c_a_p_engineer)

# License
[MIT license](https://en.wikipedia.org/wiki/MIT_License).
