<!-- toc -->

# APN設定

CANDY Pi Liteの携帯電話ネットワークへの接続先(APN)は、インストール時に指定することができます。この宛先は、インストール後に変更することが可能です。異なるMVNOのSIMカードを変更したときには、APNの変更も行うようにしましょう。

## APNの指定

CANDY Pi Liteの携帯電話ネットワークへの接続先(APN)は、`/opt/candy-line/candy-pi-lite/environment`にある以下の箇所に定義されています。

```
# LTE/3G access point name defined in `apn-list.json`
APN=soracom.io
```

このAPNを変更すると、任意のAPNに接続することができます。ただし、初期状態では以下の4つからのみ指定することができます。

- `soracom.io` ... ソラコム(3G/LTE共通)
- `lte-d.ocn.ne.jp` ... OCNモバイルONE(LTE専用)
- `3g-d-2.ocn.ne.jp` ... OCNモバイルONE(3G専用)
- `iijmio.jp` ... iij mio(3G/LTE共通)

## APNの追加

初期状態で指定できる4つのAPNに加え、ご利用の方々が任意のAPNを追加することができます。初期状態以外のMVNOや閉域網に接続するなど、任意のAPNを指定する場合は以下の手順をおこなってください。

1. `/opt/candy-line/candy-pi-lite/apn-list.json` をエディター(`vi`や`nano`など)で開きます
1. 一番最後の行で新しいデータを追加します（下記参照）
1. 中身を保存します

```
{
   "soracom.io":{"user":"sora","password":"sora"}
  ,"lte-d.ocn.ne.jp":{"user":"mobileid@ocn","password":"mobile"}
  ,"3g-d-2.ocn.ne.jp":{"user":"mobileid@ocn","password":"mobile"}
  ,"iijmio.jp":{"user":"mio@iij","password":"iij"}
<<ここに追加します>>
}
```
追加するデータの書式は以下の通りです。

```
,"APN名":{"user":"APNユーザーID","password":"APNパスワード"}
```
最初のカンマはつけておいてください。

追加したAPNを利用するには、`/opt/candy-line/candy-pi-lite/environment`の`APN`に追加したAPNを指定するようにしてください。`apn-list.json`に追加するだけでは、そのAPNを利用できません。
