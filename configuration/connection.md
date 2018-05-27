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

初期状態で接続を行わないようにした場合、接続状態は「サスペンド」状態として扱われます。接続を行うときは、次の「接続を復元するには」に記載のコマンドを実施してください。

## 接続を復元するには

接続を行うときは、以下のコマンドにより接続を実施してください。

```bash
$ sudo candy connection resume
```

## 接続を停止するには

接続を一時的に停止するには、以下のコマンドを実行して「サスペンド」状態にします。この状態では、完全にネットワークから切断された状態になります。

```bash
$ sudo candy connection suspend
```

## 接続を状態を確認するには

以下のコマンドにより、現在の接続状態を見ることができます。

```bash
$ sudo candy connection status
#=> ONLINE
```

`ONLINE`（接続中）または`OFFLINE`（接続切断中）の文字が出現します。
