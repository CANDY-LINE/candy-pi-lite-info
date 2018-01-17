<!-- toc -->

# デフォルトゲートウェイ調整機能のOFF

** 👉[`candy-pi-lite-service v1.8.0`](https://forums.candy-line.io/t/v1-8-0)以降で対応しています **

## 概要

CANDY Pi Liteで3G/LTE通信をしている状態で、ラズパイなどへEthernetケーブルを差し込むとデフォルトゲートウェイの設定が変更されます。これにより、インターネット側に出て行く経路がEthernet側に変更されます。このような設定とならないようにするために、`candy-pi-lite-service`は常に3G/LTE通信のネットワークをデフォルトゲートウェイとして利用するように常に調整しています。

一方で、このような調整を行うために、任意のデフォルトゲートウェイの設定を許容していませんでした。このため、任意のデフォルトゲートウェイを利用者の方が利用したい場合にはこれまで方法がありませんでした。

## 調整機能のON/OFF

`candy-pi-lite-service`のインストール時に以下のように`DISABLE_DEFAULT_ROUTE_ADJUSTER=0`を設定することにより、この調整機能をOFFにすることができます。標準ではONとなり（`1`を指定）、有効になります。

```bash
$ curl -sL https://git.io/v7bXx | sudo DISABLE_DEFAULT_ROUTE_ADJUSTER=0 BOOT_APN=<apn名> bash
```

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
ファイルを保存したら、[candy-pi-lite サービスを再起動](/service/restart.md)するかラズパイを再起動してください。
