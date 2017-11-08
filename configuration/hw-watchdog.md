<!-- toc -->

# ハードウェアWatchdog

** 👉[`candy-pi-lite-service v1.6.0`](https://forums.candy-line.io/t/v1-6-0/55)以降で対応しています **

## 概要

Raspberry Piには、ハードウェアの仕組みとしてシステム無応答を検知したときに自動的に再起動をする仕組みを備えています。しかし、通常その機能をは無効にされており、必要なときにだけ有効にするようになっています。

この機能を利用するために特別なソフトウェアのインストールは不要です。ただし、OSは Raspbian Stretch 以降でなければなりません。

もし意図せずに有効にしてしまっても、以下に記載する設定無効化方法を実施することにより無効にすることが可能です。

## 設定方法

candy-pi-liteサービスをインストールするときに、`ENABLE_WATCHDOG=1`を指定してください。手動で設定したい場合は、こちらの[投稿](https://www.raspberrypi.org/forums/viewtopic.php?t=175432#p1119436)を参照してください。

## 設定確認方法

フォークボムと呼ばれる下記のコマンドを実行するとシステム再起動を確認することができます。ただし、ハードウェアWatchdogを設定せずにコマンドを実行すると、著しく動作が遅くなり制御不能になったりするため電源をOFFにする以外に方法はなくなりますのでご注意ください。

```
:(){ :|: & };:
```

## 設定無効化方法

ハードウェアWatchdogの設定を無効にするには、まず`/boot/config.txt`ファイルの以下の内容を見つけてください。

```
dtparam=watchdog=on
```

続いて上記の値を以下のように変更します。

```
dtparam=watchdog=off
```

ファイルを保存してRaspbianを再起動させてください。