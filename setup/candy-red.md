<!-- toc -->

# CADNY RED単体のインストール

candy-pi-lite サービスをインストールすると、ラズパイ上にNode-REDベースのフローエディターである[CANDY RED](https://github.com/CANDY-LINE/candy-red)もインストールされます。通常のNode-REDとしての機能のほか、CANDY EGGクラウドサービスと連携して手軽にクラウドとのやりとりを行うアプリケーションを作成することができます。

> ### <☝️ワンポイント> Node-REDに馴染みのない方にオススメの書籍
>
> 2017年に以下の2種類の書籍が発売されました。Node-REDの解説がされています。CANDY REDはNode-REDをベースにしているため、これらの書籍が参考になります。
>
> - プログラミング初心者の方へ：[つないで つないで プログラミング Node-REDでつくる初めてのアプリ](https://www.amazon.co.jp/%E3%81%A4%E3%81%AA%E3%81%84%E3%81%A7-%E3%83%97%E3%83%AD%E3%82%B0%E3%83%A9%E3%83%9F%E3%83%B3%E3%82%B0-Node-RED%E3%81%A7%E3%81%A4%E3%81%8F%E3%82%8B%E5%88%9D%E3%82%81%E3%81%A6%E3%81%AE%E3%82%A2%E3%83%97%E3%83%AA-%E6%97%A5%E7%AB%8B-Node-RED%E3%82%A8%E3%83%90%E3%83%B3%E3%82%B8%E3%82%A7%E3%83%AA%E3%82%B9%E3%83%88/dp/486594107X/ref=pd_bxgy_14_img_2?_encoding=UTF8&psc=1&refRID=SFBN3VN5CEB3HPJ1MSZ3)
> - プログラミングの心得のある方へ：[はじめてのNode‐RED](https://www.amazon.co.jp/%E3%81%AF%E3%81%98%E3%82%81%E3%81%A6%E3%81%AENode%E2%80%90RED-I%E3%83%BB-BOOKS-Node%E2%80%90RED%E3%83%A6%E3%83%BC%E3%82%B6%E3%83%BC%E3%82%B0%E3%83%AB%E3%83%BC%E3%83%97%E3%82%B8%E3%83%A3%E3%83%91%E3%83%B3/dp/4777520269/ref=sr_1_1?s=books&ie=UTF8&qid=1510564607&sr=1-1&keywords=%E3%81%AF%E3%81%98%E3%82%81%E3%81%A6%E3%81%AENode%E2%80%90RED+%28I%E3%83%BBO+BOOKS%29&dpID=51preNH1xkL&preST=_SY291_BO1,204,203,200_QL40_)

初回インストール時に[CANDY RED](https://github.com/CANDY-LINE/candy-red)を **インストールしていない場合(`CANDY_RED=0`を指定してインストールした場合)** 以下の手順で追加することができます。すでにインストールされているときは、以下の手順は不要となります。

### CANDY REDアプリケーションのインストール

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

続いて、Node.jsを入れ替えます。Raspbian 4.1以降ではNode-REDがプリインストールされていますのでNode.jsもすでに入っています。しかし、[CANDY RED](https://github.com/CANDY-LINE/candy-red)インストール時に追加するアドオンを用意するときに、プリインストールされたNode.jsでは解決できないエラーが発生してしまいます。これを避けるため、Node.jsを入れ替えるようにします。

Raspberry Pi Model B+をお使いの場合は、以下のコマンドを実行します。
```bash
$ sudo apt-get update -y
$ sudo apt-get upgrade -y
$ cd /tmp
$ ARMv6_NODEJS_VERSION="6.11.2"
$ wget https://nodejs.org/dist/v${ARMv6_NODEJS_VERSION}/node-v${ARMv6_NODEJS_VERSION}-linux-armv6l.tar.gz
$ tar zxf node-v${ARMv6_NODEJS_VERSION}-linux-armv6l.tar.gz
$ cd node-v${ARMv6_NODEJS_VERSION}-linux-armv6l/
$ sudo cp -R * /usr/local/
$ sudo apt-get install -y python-dev python-rpi.gpio bluez libudev-dev
```

Raspberry Pi 2と3をお使いの場合は、以下のコマンドを実行します。
```bash
$ sudo apt-get update
$ sudo apt-get upgrade
$ curl -sL https://deb.nodesource.com/setup_6.x | sudo bash -
$ sudo apt-get install -y python-dev python-rpi.gpio bluez nodejs libudev-dev
```

続いて`npm`のキャッシュをクリアしておきましょう。そうしないと、古いバージョンを見てしまうかもしれないからです。
```
$ sudo npm cache clean
```

それでは[CANDY RED](https://github.com/CANDY-LINE/candy-red)をインストールしましょう。インストールには、15分~30分ほどかかります。`--max-old-space-size=128`には、Node.jsプロセスが割り当てられる上限のメモリーサイズを指定しましょう。デフォルトでは512MiBとなり、Raspberry Piの機種によっては、大きすぎる値になる場合がありますので、最大容量よりも少ない値となるように指定しましょう。この例では、128を割り当てています。

```bash
$ sudo NODE_OPTS=--max-old-space-size=128 npm install -g --unsafe-perm candy-red
```

### CANDY REDの動作確認

それでは動作しているかを確認します。
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

ノードの追加などの方法は[CANDY REDでのノード設定](/configuration/)をご覧ください。
