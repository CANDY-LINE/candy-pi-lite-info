<!-- toc -->

# デフォルトゲートウェイ調整機能のOFF

** 👉[`candy-pi-lite-service v1.8.0`](https://forums.candy-line.io/t/v1-8-0)以降で対応しています **

## 概要

CANDY Pi Liteで3G/LTE通信をしている状態で、ラズパイなどへEthernetケーブルを差し込むとデフォルトゲートウェイの設定が変更されます。これにより、インターネット側に出て行く経路がEthernet側に変更されます。このような設定とならないようにするために、`candy-pi-lite-service`は常に3G/LTE通信のネットワークをデフォルトゲートウェイとして利用するように常に調整しています。

一方で、このような調整を行うために、任意のデフォルトゲートウェイの設定を許容していませんでした。このため、任意のデフォルトゲートウェイを利用者の方が利用したい場合にはこれまで方法がありませんでした。

**ご注意）調整機能をOFFにした場合に期待通りにネットワークを動作させるには、`ip`コマンドの知識やネットワーク設定の知識が必要です。不明な場合は、本機能をOFFにしないようにしてください。**

## インストール時の調整機能ON/OFF

`candy-pi-lite-service`のインストール時に以下のように`DISABLE_DEFAULT_ROUTE_ADJUSTER=0`を設定することにより、この調整機能をOFFにすることができます。標準ではONとなり（`1`を指定）、有効になります。

```bash
$ curl -sL https://git.io/v7bXx | sudo DISABLE_DEFAULT_ROUTE_ADJUSTER=0 BOOT_APN=<apn名> bash
```

## インストールした後に変更する方法

また、**インストールした後** で挙動を変更したい場合は、以下のように環境変数ファイルを開きます。

```bash
$ sudo nano /opt/candy-line/candy-pi-lite/environment
```

すると以下のような箇所がありますので、
```
# Set 1 for disabling default route adjuster
DISABLE_DEFAULT_ROUTE_ADJUSTER=1
```

`1`の代わりに`0`を指定します。
```
DISABLE_DEFAULT_ROUTE_ADJUSTER=0
```
ファイルを保存したら、[candy-pi-lite サービスを再起動](/service/restart.md)するかシステムを再起動してください。

## 調整機能をOFFにした場合の注意

通常、以下の例のようにデフォルトルートは`ppp0`に割当たります。

```
$ ip route
default dev ppp0 scope link
10.64.64.64 dev ppp0 proto kernel scope link src 10.160.153.211
192.168.2.0/24 dev eth0 proto kernel scope link src 192.168.2.3 metric 202
```

しかし、Ethernetケーブルを抜き差しすると、以下のようにデフォルトゲートウェイの設定が変更されます。

```
default dev ppp0 scope link
default via 192.168.2.1 dev eth0 src 192.168.2.3 metric 202
10.64.64.64 dev ppp0 proto kernel scope link src 10.160.153.211
192.168.2.0/24 dev eth0 proto kernel scope link src 192.168.2.3 metric 202
```

このため、Ethernetケーブルを差し込んでいる間も`ppp0`のデフォルトゲートウェイを利用したいときは、明示的に`ip`コマンドでEthernetのデフォルトゲートウェイを削除してください。
