<!-- toc -->

# CADNY REDのバージョンアップ

CANDY REDのバージョンアップは、[CANDY REDのインストール](/setup/candy-red.md)と似たような手順で行います。

バージョンアップ後にも、フローファイルはそのまま利用できますが、念のためフローファイルをバックアップしておくことをお勧めします。

### パッケージのアップデート

まず最初に、candy-pi-lite サービスを停止し、LANケーブルまたはWiFiでインターネットに接続します。これは、ダウンロードにかかる通信を携帯電話ネットワークではなく有線・無線LANにて行うようにするためです。

はじめに、以下のコマンドを実行してcandy-pi-lite サービスを停止します。

```bash
$ sudo systemctl stop candy-pi-lite
```

続いて、ネットワークの確認を行います。ラズパイにコマンドラインからアクセスして、以下のコマンドを実行します。

```bash
$ curl --head https://registry.npmjs.org
```

以下のように結果が返って来るようであれば、正しくインターネットに接続できています。

```
HTTP/1.1 200 OK
server: CouchDB/1.5.0 (Erlang OTP/R16B03)
Content-Type: application/json
Cache-Control: max-age=300
Content-Length: 262
Accept-Ranges: bytes
Date: Fri, 16 Sep 2016 05:19:25 GMT
Via: 1.1 varnish
Age: 108
Connection: keep-alive
X-Served-By: cache-hkg6823-HKG
X-Cache: HIT
X-Cache-Hits: 1
X-Timer: S1474003165.840989,VS0,VE0
Vary: Accept-Encoding
```

続いて`npm`のキャッシュをクリアしておきましょう。そうしないと、古いバージョンを見てしまうかもしれないからです。
```
$ sudo npm cache clean
```

それでは[CANDY RED](https://github.com/CANDY-LINE/candy-red)をアップデートしましょう。アップデートには、インストールと同様に15分~30分ほどかかる場合もあります。また、インストール時と同じように、`NODE_OPTS`も指定してください。

```bash
$ sudo NODE_OPTS=--max-old-space-size=128 npm install -g --unsafe-perm candy-red
```

もし、なんらかの事情で特定のバージョンをインストールしたいときは、以下のようにバージョンを指定してください。

```bash
$ sudo NODE_OPTS=--max-old-space-size=128 npm install -g --unsafe-perm candy-red@バージョン
```

`バージョン`には、例えば`5.0.0`のような形式の文字列を指定します。無効な文字列を指定するとインストールできません。


### CANDY REDの動作確認

インストールが終わったら、[CANDY RED](https://github.com/CANDY-LINE/candy-red)が動作しているかを確認します。
```bash
$ sudo systemctl status candy-red
```

上記を実行して、以下のような結果が得られれば問題ありません。

    ● candy-red.service - CANDY RED Gateway Service, version:
       Loaded: loaded (/lib/systemd/system/candy-red.service; enabled)
       Active: active (running) since Wed 2016-01-27 02:11:31 UTC; 594ms ago
     Main PID: 3612 (bash)
       CGroup: /system.slice/candy-red.service
               ├─3612 bash /usr/local/lib/node_modules/candy-red/services/start_systemd.sh
               └─3618 node --max-old-space-size=128 /usr/local/lib/node_modules/candy-red/dist/index.j...

    Jan 27 02:11:31 my-ltepi systemd[1]: Starting CANDY RED Gateway Service, version:...
    Jan 27 02:11:31 my-ltepi systemd[1]: Started CANDY RED Gateway Service, version:.
    Jan 27 02:11:31 my-ltepi start_systemd.sh[3612]: logger: Activating Bluetooth...
    Jan 27 02:11:31 my-ltepi start_systemd.sh[3612]: Can't get device info: No such device
    Jan 27 02:11:31 my-ltepi start_systemd.sh[3612]: logger: Starting candy-red...

なお、この時点で、端末を再起動したときには、自動的に[CANDY RED](https://github.com/CANDY-LINE/candy-red)が起動するようになります。

続いて、candy-pi-lite サービスを再度起動しましょう。
```bash
$ sudo systemctl start candy-pi-lite
```

1〜2分ほどで、モデムが起動しインターネットに接続します。以下のコマンドを実行して接続状況を確認することができます。

```bash
$ ip route | grep default
```

以下のように`ppp0`と出ていれば成功です。
```
default dev ppp0  scope link
```

最後に[CANDY REDへのブラウザー接続](browsing-candy-red.md)を参照して、ブラウザーから接続してみましょう。

ブラウザーから以下のようにバージョンを見ることができます。

![CANDY REDバージョン](/assets/candy-red-version.png)
