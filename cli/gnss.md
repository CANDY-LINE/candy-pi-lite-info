# GNSS/GPSの制御

## GPSの起動

初期状態では、GPSの機能は停止状態になっています。GPSを使うときは、GPSの起動を明示的に行う必要があります。
OS起動時に常に起動させたい時は、[こちらの「インストールした後にGNSS自動起動設定を変更する方法」](/configuration/gnss.md)をご覧ください。

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
