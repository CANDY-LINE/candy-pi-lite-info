## GNSS/GPSの使用

** 👉[`candy-pi-lite-service v5.0.0`](https://forums.candy-line.io/t/v5-0-0)以降で対応しています **

CANDY Pi Lite 3GとCANDY Pi Lite+では、専用のアンテナを取り付けることによりGPSの機能を使用することができます。コマンドラインまたは[CANDY RED](https://github.com/CANDY-LINE/candy-red)を使用して、GPSの機能を利用することが可能です。GPSの情報は、JSON形式での取得または、NMEAフォーマットのデータの連続出力を得ることが可能です。

[CANDY RED](https://github.com/CANDY-LINE/candy-red)を使用すると、専用のソフトウェアを用意せずにGPSの機能を使ったアプリケーションを作成することができます。詳細については、フォーラムにて投稿予定です。

この利用ガイドでは、コマンドラインによる使い方を解説します。

## 対応しているGNSS種類

CANDY LINEのソフトウェアでは、`GPS`のみサポートします。`GPS`以外をご利用になりたい方は、通信モジュールの技術ドキュメントをご覧になり、直接ATコマンドを操作してご利用ください。なお、`GPS`以外の利用については、CANDY LINEではサポートしておりません。

## GPSの起動

初期状態では、GPSの機能は停止状態になっています。GPSを使うときは、GPSの起動を明示的に行う必要があります。

```bash
$ sudo candy gnss start
```

CANDY Pi Lite/CANDY Pi Lite+とラズパイまたはASUS Tinker Boardを接続している時は、一度起動すると明示的に停止させるまで起動し続けます。ただし、GNSS電波が不通の状態が続く場合は停止することがあります。

UART接続（USB接続なし）で通信中の場合は、以下のように`--suspend --resume`をつけてください。

```bash
$ sudo candy gnss start　--suspend --resume
```

これによって、一時的に接続を中断し、GPSを起動してから接続を再開します。接続が停止する時間は、電波環境が良ければ4G/LTEであれば6秒前後、3Gでは10秒前後となります。

## GPSの停止

GPSの動作を止める場合は、以下のコマンドを実行します。

```bash
$ sudo candy gnss stop
```

UART接続（USB接続なし）で通信中の場合は、以下のように`--suspend --resume`をつけてください。

```bash
$ sudo candy gnss stop--suspend --resume
```

## GPSの起動状態確認

GPSの起動状態を見るには、以下のコマンドを実行します。

```bash
$ sudo candy gnss status
```

UART接続（USB接続なし）で通信中の場合は、以下のように`--suspend --resume`をつけてください。

```bash
$ sudo candy gnss status --suspend --resume
```

## コマンドによるGPSの位置取得

GPSの位置情報をコマンドラインから取得することができます。

```bash
$ sudo candy gnss locate
```

結果は、以下のようなJSON形式の文字列が返ります。

```
{
  "timestamp": "2018-05-23T04:26:44.000Z",
  "latitude": 35.00000,
  "longitude": 139.00000,
  "altitude": 54.8,
  "cog": 132.3,
  "spkm": 0.0,
  "spkn": 0.0,
  "nsat": 7,
  "hdop": 0.9,
  "fix": "2D"
}
```

- `timestamp` ... ISO8601フォーマットの日付(UTC)
- `latitude` ... 緯度 (°)
- `longitude` ... 経度 (°)
- `altitude` ... 高度 (m)
- `cog` ... 進行方向(真北からの角度)
- `spkm` ... 対地速度(km/h)
- `spkn` ... 対地速度(knots)
- `nsat` ... 受信衛星数
- `hdop` ... 水平位置精度劣化度(0.5~99.9)
- `fix` ... GNSS測位モード(2Dまたは3D)

UART接続（USB接続なし）で通信中の場合は、以下のように`--suspend --resume`をつけてください。

```bash
$ sudo candy gnss locate --suspend --resume
```

## NMEAによるGPSの位置取得

USB接続時には、NMEAセンテンス専用のシリアルポート`/dev/QWS.UC20.NMEA`、または`/dev/QWS.EC25.NMEA`を利用することができます。ボーレートは、9600bpsとなります。それぞれ、次の機種に対応します。

- `/dev/QWS.UC20.NMEA` ... CANDY Pi Lite 3G
- `/dev/QWS.EC25.NMEA` ... CANDY Pi Lite+

**👉 CANDY Pi Lite LTEモデルでは対応していません。**

本機能は、NMEA（NMEA 0183）について予備知識のある方向けの機能となります。NMEAの詳細については本書では扱いませんので、ご利用者の方にて予めお調べの上お使いください。`cgps`コマンドを使った例は、フォーラムにて投稿予定です。

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
