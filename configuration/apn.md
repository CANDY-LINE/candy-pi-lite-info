<!-- toc -->

# APN設定

CANDY Pi Liteの携帯電話ネットワークへの接続先(APN)は、インストール時に指定することができます。この宛先は、インストール後に変更することが可能です。異なるMVNOのSIMカードを変更したときには、APNの変更も行うようにしましょう。

[`candy-pi-lite-service v1.7.0`](https://forums.candy-line.io/t/v1-7-0/63)からAPNの指定方法が簡単になりました。以前のバージョンをご利用の場合は、本章の後半をご覧ください。

## APNの指定

** 👉[`candy-pi-lite-service v1.7.0`](https://forums.candy-line.io/t/v1-7-0/63)以降で対応しています **

APNを指定するには、パソコンなどでマイクロSDカードの`/boot`ディレクトリーに`apn`という名前のファイルを作成します。ファイルの中身は、APNの名称を指定します。初期状態では、以下の名称を利用可能です。

- `soracom.io` ... ソラコム(3G/LTE共通)
- `lte-d.ocn.ne.jp` ... OCNモバイルONE(LTE専用)
- `3g-d-2.ocn.ne.jp` ... OCNモバイルONE(3G専用)
- `iijmio.jp` ... iij mio(3G/LTE共通)

例えば、ソラコムのSIMをご利用の場合は、メモ帳やテキストエディターなどで`soracom.io`とだけ入力し保存します。

その後、そのマイクロSDを利用してRaspberryPiを起動してください。すると自動的にそのAPNが選択されるようになります。また、`/boot`に保存したファイルはAPNの設定が成功すると削除されます。

ただし、APNに上記以外のAPNを指定した時は、エラーとなり`/boot`に保存した`apn`ファイルはそのまま削除されずに残ったままとなります。

## APNの追加

** 👉[`candy-pi-lite-service v1.7.0`](https://forums.candy-line.io/t/v1-7-0/63)以降で対応しています **

APNを追加する場合も、`/boot`ディレクトリーに`apn`という名前のファイルを作成して追加することができるようになりました。この場合は、以下のようにAPNの他、ユーザーIDとパスワードも指定しなければなりません。また、JSON形式ですので書式が間違っていると正しく追加されませんのでご注意ください。エラーとなった場合は、先程と同様に、`/boot/apn`のファイルは削除されずに残されています。

また、エラーメッセージについては、`/var/log/syslog`にも表示されますので、うまく設定されない場合はこのログをご確認ください。

APNを追加したい場合の`apn`ファイルの中身は以下のような書式になります。
```
{
  "apn": "APN",
  "user": "ユーザーID",
  "password": "パスワード"
}
```

上記のうち、`APN`、`ユーザーID`、`パスワード`の部分を書き換えてください。ダブルクォーテーション「"」はそのまま残しておいてください。

## APNの指定 *（v1.7.0より古い場合）*

** 👉[`candy-pi-lite-service v1.7.0`](https://forums.candy-line.io/t/v1-7-0/63)以降ではより簡単な方法をご利用いただけます **

CANDY Pi Liteの携帯電話ネットワークへの接続先(APN)は、`/opt/candy-line/candy-pi-lite/environment`にある以下の箇所に定義されています。

```
# LTE/3G access point name defined in `apn-list.json`
APN=soracom.io
```

**ご注意：最初に`soracom.io`以外のAPNを指定した場合は、上記には指定されたAPNが書かれています。**

このAPNを変更すると、任意のAPNに接続することができます。ただし、初期状態では以下の4つからのみ指定することができます。

- `soracom.io` ... ソラコム(3G/LTE共通)
- `lte-d.ocn.ne.jp` ... OCNモバイルONE(LTE専用)
- `3g-d-2.ocn.ne.jp` ... OCNモバイルONE(3G専用)
- `iijmio.jp` ... iij mio(3G/LTE共通)

## APNの追加 *（v1.7.0より古い場合）*

** 👉[`candy-pi-lite-service v1.7.0`](https://forums.candy-line.io/t/v1-7-0/63)以降ではより簡単な方法をご利用いただけます **

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
