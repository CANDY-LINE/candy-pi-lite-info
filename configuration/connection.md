# モバイルネットワークへの接続設定

ここでは、OS起動時のモバイルネットワークへの接続を行うかどうかの設定について説明します。
モバイルネットワークへの接続停止や再開は、[こちらのコマンドライン](/cli/connection.md)にて実施可能です。

## 起動時の接続設定

** 👉[`candy-pi-lite-service v5.0.0`](https://forums.candy-line.io/t/v5-0-0)以降で対応しています **

通常、CANDY Pi Lite/CANDY Pi Lite+が起動した時には、常にモバイルネットワークへ接続します。この動作を初期状態で接続させないように指定することができます。

## インストール時の接続設定

`candy-pi-lite-service`のインストール時に以下のように`CONNECT_ON_STARTUP=0`を設定することにより、初期状態で接続させないようにすることができます。標準では接続するようになっています（`1`が指定される）。

```bash
$ curl -sL https://git.io/v7bXx | sudo CONNECT_ON_STARTUP=0 BOOT_APN=<apn名> bash
```

## インストールした後に変更する方法

また、**インストールした後** で挙動を変更したい場合は、以下のように環境変数ファイルを開きます。

```bash
$ sudo nano /opt/candy-line/candy-pi-lite/environment
```

すると以下のような箇所がありますので、
```
# Set 1 for establishing a connection on start-up
CONNECT_ON_STARTUP=1
```

`1`の代わりに`0`を指定します。
```
CONNECT_ON_STARTUP=0
```
ファイルを保存したら、[candy-pi-lite サービスを再起動](/service/restart.md)するかシステムを再起動してください。

## 初期状態で接続を行わない場合の注意

初期状態で接続を行わないようにした場合、接続状態は「サスペンド」状態として扱われます。接続を行うときは、「[モバイルネットワーク接続の制御](/cli/connection.rd)」の「モバイルネットワーク接続を再開する場合」に記載の`candy connection resume`コマンドを実施してください。
