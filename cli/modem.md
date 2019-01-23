<!-- toc -->

# 通信モジュール（モデム）情報の表示

通信モジュールに関する情報を表示することができます。また、EC21をお使いの場合は、パケットカウンターの値を表示することができます。

## 情報表示のコマンド

** 👉[`candy-pi-lite-service v6.3.0`](https://forums.candy-line.io/t/candy-pi-lite-v6-3-0)以降で対応しています **

通信モジュールの情報を表示するには、以下のコマンドを実行してください。

```bash
$ sudo candy modem show
```

UART接続（USB接続なし）で通信中の場合は、以下のように`--suspend --resume`をつけてください。これらのオプションをつけ忘れると`Modem is not ready`と表示されたり、結果が表示された後で再接続が行われないことがあります。

```bash
$ sudo candy modem show --suspend --resume
```

実行すると以下のような結果が表示されます。

```bash
{
  "counter": {
    "rx": "0",
    "tx": "0"
  },
  "datetime": "17/08/19,04:02:57",
  "imei": "000000000000000",
  "timezone": 9.0,
  "model": "UC20",
  "revision": "UC20GQBR03A14E1G",
  "manufacturer": "Quectel"
}
```

### 結果の説明

- `counter` ... パケットカウンターの値です。単位はバイトです。UC20では常に0となります
- `datetime` ... 通信モジュール内の時刻です
- `timezone` ... 通信モジュール内のタイムゾーンです
- `model` ... 通信モジュールの機種名です
- `revision` ... 通信モジュールファームウェアのバージョンです
- `manufacturer` ... 通信モジュールのメーカー名です
