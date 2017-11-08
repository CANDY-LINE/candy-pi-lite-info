<!-- toc -->

# EnOcean USBゲートウェイの利用

** 👉[`candy-pi-lite-service v1.6.0`](https://forums.candy-line.io/t/v1-6-0/55)以降で対応しています **

## 概要

EnOcean USBゲートウェイをRaspberry Piに接続すると、通常`/dev/ttyUSB0`などのパスでシリアルポートが割り当てられます。このパスの番号の箇所は、OSが認識した順序で自動的に番号が割り当てられます。したがって、複数のUSB機器を接続した場合に常にEnOceanを利用したいという場合に、期待したシリアルポートのパスを利用できない場合があります。

このような事態を避けるために、`candy-pi-lite-service`では、EnOceanのUSBゲートウェイが認識された時に、固定の名称`/dev/enocean`を利用できるような設定を行うようにしています。

## 設定の有効化・無効化

本設定は自動的に有効になります。また、`candy-pi-lite-service`をアンインストールすると自動的に無効になります。

この設定を行いたくない場合は、以下のいずれかの方法で無効にすることができます。

1. インストールする時に`COFIGURE_ENOCEAN_PORT=0`を指定してインストールする
1. すでにインストールしているときは、ファイル`/etc/udev/rules.d/99-enocean-stick.rules`を削除する
