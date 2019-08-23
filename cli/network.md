<!-- toc -->

# ネットワーク状態の表示

現在のネットワークに関する情報を表示することができます。

## 情報表示のコマンド

** 👉[`candy-pi-lite-service v6.3.0`](https://forums.candy-line.io/t/candy-pi-lite-v6-3-0)以降で対応しています **

ネットワークやその状態に関する情報を表示するには、以下のコマンドを実行してください。

```bash
$ sudo candy network show
```

UART接続（USB接続なし）で通信中の場合は、以下のように`--suspend --resume`をつけてください。これらのオプションをつけ忘れると`Modem is not ready`と表示されたり、結果が表示された後で再接続が行われないことがあります。

```bash
$ sudo candy network show --suspend --resume
```

実行すると以下のような結果が表示されます（3G版をお使いの場合は、`eps`の値は`N/A`となります）。

```bash
{
  "network": "N/A",
  "access": "FDD LTE",
  "band": "LTE BAND 1",
  "registration": {
    "cs": "Unregistered",
    "ps": "Registered",
    "eps": "Registered"
  },
  "operator": "NTT DOCOMO NTT DOCOMO",
  "rssi": "-79",
  "rssiDesc": ""
}
```

### 結果の説明

- `network` ... 常に`N/A`を返します。接続状態を知るには、[`connection status`](connection.md)コマンドを利用してください
- `access` ... 無線アクセス技術の種類を示します。`FDD LTE`や`WCDMA`といった値が返ります
- `band` ... 接続している周波数バンドが表示されます。`LTE BAND 1`や`WCDMA 800`といった値が返ります。LTEの場合はLTE BAND 43までの番号が表示されます
- `registration` ... 無線設備への登録状態に関する情報です。`cs`はSMS/音声通信への接続状態を示し、`ps`はデータ通信への接続状態を、また`eps`はLTEのデータ通信への接続状態をそれぞれ示します
- `operator` ... 接続している携帯電話ネトワークオペレーター（通信キャリア）の識別名です
- `rssi` ... 電波強度を表します。単位は、dBmです
- `rssiDesc` ... 電波強度が`rssi`の値より小さいか、より大きいか、電波が検出できない場合にその旨の説明が追加されます。`OR_LESS` は、`rssi`の値未満であることを示します。`OR_MORE`、`rssi`の値より大きいことを示します
