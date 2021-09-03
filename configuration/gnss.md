## GNSS/GPSの使用

**👉[`candy-pi-lite-service v5.0.0`](https://forums.candy-line.io/t/v5-0-0)以降で対応しています**

CANDY Pi Lite 3GとCANDY Pi Lite+では、専用のアンテナを取り付けることによりGPSの機能を使用することができます。コマンドラインまたは[CANDY RED](https://github.com/CANDY-LINE/candy-red)を使用して、GPSの機能を利用することが可能です。GPSの情報は、JSON形式での取得または、NMEAフォーマットのデータの連続出力を得ることが可能です。

ただし、初期状態では、GNSS/GPSが起動していませんので、[コマンドライン](/cli/gnss.md)で明示的に起動するか、後述のGNSS自動起動を設定しておく必要があります。

[CANDY RED](https://github.com/CANDY-LINE/candy-red)を使用すると、専用のソフトウェアを用意せずにGPSの機能を使ったアプリケーションを作成することができます。詳細については、フォーラムにて投稿予定です。

GNSS/GPS機能をコマンドラインで起動、停止、状態確認、位置取得を行う場合は、[こちらのページ](/cli/gnss.md)をご覧ください。

## 対応しているGNSS種類

GPSのほか、QZSS（みちびき）を利用可能です。モジュールの仕様により、QZSS（みちびき）を有効にするとGalileo、GLONASS、北斗も有効になります。
ただし、GPSとQZSS（みちびき）以外の利用については、CANDY LINEでは未確認であり、サポートもしておりません。

**ご注意**
- QZSS（みちびき）は、CANDY Pi Lite+シリーズのみ利用可能です。

## NMEAによるGPSの位置取得

USB接続時には、NMEAセンテンス専用のシリアルポート`/dev/QWS.UC20.NMEA`、または`/dev/QWS.EC25.NMEA`を利用することができます。ボーレートは、9600bpsとなります。それぞれ、次の機種に対応します。

- `/dev/QWS.UC20.NMEA` ... CANDY Pi Lite 3G
- `/dev/QWS.EC25.NMEA` ... CANDY Pi Lite+

**👉 CANDY Pi Lite LTEモデルでは対応していません。**

本機能は、NMEA（NMEA 0183）について予備知識のある方向けの機能となります。NMEAの詳細については本書では扱いませんので、ご利用者の方にて予めお調べの上お使いください。`cgps`コマンドを使うとターミナル上でNMEAの情報を簡易に見ることが可能です。詳しくは、[こちらの投稿](https://forums.candy-line.io/t/gpsd/172/5)を参照してください。

## インストール時にGNSS自動起動を設定するには

`candy-pi-lite-service`のインストール時に以下のように`GNSS_ON_STARTUP=1`を設定することにより、初期状態では、GNSSを起動しないようになっています（`0`が指定される）。

```bash
$ curl -sL https://git.io/v7bXx | sudo GNSS_ON_STARTUP=1 BOOT_APN=<apn名> bash
```

## インストールした後にGNSS自動起動設定を変更する方法

また、**インストールした後** で挙動を変更したい場合は、以下のように環境変数ファイルを開きます。

```bash
$ sudo nano /opt/candy-line/candy-pi-lite/environment
```

すると以下のような箇所がありますので、
```
# Set 1 for starting GNSS session on start-up
GNSS_ON_STARTUP=0
```

`0`の代わりに`1`を指定します。
```
GNSS_ON_STARTUP=1
```
ファイルを保存したら、[candy-pi-lite サービスを再起動](/service/restart.md)するかシステムを再起動してください。

## QZSS（みちびき）を自動起動時に有効にする方法
**👉[`candy-pi-lite-service v10.4.0`](https://forums.candy-line.io/t/v10-4-0)以降で対応しています**

QZSS（みちびき）を有効にしたいときは、`1`の代わりに`2`または`3`を指定します。
```
GNSS_ON_STARTUP=2
```
値の意味は以下の通りです。どちらの値もQZSS（みちびき）を有効にできますが、同時に有効となるGNSSサービスの種類が異なります。

- `2`・・・QZSS（みちびき）を有効にします。同時に、GLONASSと北斗も有効になります（これら2つは無効にできません）
- `3`・・・QZSS（みちびき）を有効にします。同時に、Galileo、GLONASS、北斗も有効になります（これら3つは無効にできません）

ファイルを保存したら、[candy-pi-lite サービスを再起動](/service/restart.md)するかシステムを再起動してください。

**ご注意**
- QZSS（みちびき）は、CANDY Pi Lite+シリーズのみ利用可能です。
