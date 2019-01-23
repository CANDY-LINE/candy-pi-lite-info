<!-- toc -->

# SIMカード認識状態の表示

現在検出されているSIMカードの状態やその情報を表示することができます。

## 情報表示のコマンド

** 👉[`candy-pi-lite-service v6.3.0`](https://forums.candy-line.io/t/candy-pi-lite-v6-3-0)以降で対応しています **

SIMカードの状態やその情報を表示するには、以下のコマンドを実行してください。

```bash
$ sudo candy sim show
```

UART接続（USB接続なし）で通信中の場合は、以下のように`--suspend --resume`をつけてください。これらのオプションをつけ忘れると`Modem is not ready`と表示されたり、結果が表示された後で再接続が行われないことがあります。

```bash
$ sudo candy sim show --suspend --resume
```

実行すると以下のような結果が表示されます。

```bash
{
  "msisdn": "000111112222",
  "state": "SIM_STATE_READY",
  "imsi": "440100000000000"
}
```

**ご注意：ソラコムグローバルSIMなど一部のSIMカードには、電話番号(`msisdn`)がSIMカードの書かれていないことがあります。その場合は、`msisdn`には電話番号が表示されません。**

### 結果の説明

- `msisdn` ... 電話番号(MSISDN)です
- `state` ... SIMカードの認識状態を表します。`SIM_STATE_READY`であれば認識されています
- `imsi` ... SIMカードに関連づけられているIMSI番号です
