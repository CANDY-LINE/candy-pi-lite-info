<!-- toc -->

# シリアルポートの種別選択指定

** 👉[`candy-pi-lite-service v2.0.0`](https://forums.candy-line.io/t/v2-0-0)以降で対応しています **

candy-pi-lite-serviceの初期設定では、シリアルポートの選択を自動で行います。順番は、USBシリアルポートを探索し、なければUARTシリアルポートを探します。常にUSB拡張ボードを使ったUSB接続で利用される場合は、このような探索動作を行うことは冗長です。このため、candy-pi-lite-serviceにUSBのシリアルポートだけを探すように指定することが可能です。

一方で、USB接続を行なった状態でUARTの検証を行うこともあるかもしれません。そのような場合は、物理的にUSBケーブルを取り外さずに、UARTシリアルだけを接続に使うようにcandy-pi-lite-serviceへ指定することができます。

## インストール時に指定する方法

candy-pi-lite-serviceのインストール時に以下のように`SERIAL_PORT_TYPE=種別`を設定することにより、任意の種別を指定することができます。

```bash
$ curl -sL https://git.io/v7bXx | sudo SERIAL_PORT_TYPE=種別 bash
```

利用可能な「種別」の値は以下の通りです。

- `auto` ... 自動選択（初期設定）
- `usb`  ... USBシリアル接続のみ使用
- `uart` ... UARTシリアル接続のみ使用

`usb`または`uart`を指定した時に、candy-pi-lite-serviceがそれぞれの方法でシリアルポートを見つけられない時は、接続を開始しませんのでご注意ください。

## インストールした後に種別を指定する方法

**インストールした後** で挙動を変更したい場合は、以下のように環境変数ファイルを開きます。

```bash
$ sudo nano /opt/candy-line/candy-pi-lite/environment
```

すると以下のような箇所がありますので、
```
# 'auto' for automatic serial port selection, 'usb' for USB serial use only, 'uart' for ignoring USB serial
SERIAL_PORT_TYPE=auto
```

`auto`の代わりに上記の任意の値を指定します。以下は、`usb`を指定した場合の例です。
```
SERIAL_PORT_TYPE=usb
```
ファイルを保存したら、[candy-pi-lite サービスを再起動](/service/restart.md)するかシステムを再起動してください。
