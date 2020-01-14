<!-- toc -->

# 既存SDカードを利用したセットアップ

**👉 本手順は、ラズパイ、ASUS Tinker Board(またはS)共通の手順です**

**👉 ラズパイをご利用の方は、セットアップ済みのRaspbian Stretch LiteベースのOSイメージもご利用いただけます。方法は[こちらのブログ記事](https://candy-line.tumblr.com/post/167761781228/candy-pi-lite-os-image-etcher)や、「[OSイメージファイルを利用したセットアップ](/setup/etcher.md)」をご覧ください**

## コマンド入力の準備

最初にLANケーブルの一方をラズパイまたはASUS Tinker Board(またはS)に、もう一方をブロードバンドルーターに接続してインターネットに通信できる状態にしてください。電源はこの時点ではまだ入れないでください。

すでにラズパイまたはASUS Tinker Board(またはS)にてWi-Fiの設定を行っており、インターネットを利用できている場合は、Wi-Fi経由でこれ以降の作業を行うことも可能です。ただし、Wi-Fi環境では、無線状況により接続が不安定になる場合もありますので、Wi-Fi環境でうまくいかない場合は、LANケーブルを使ってインストールをお試しください。

次に、CANDY Pi Liteを取り付けたラズパイまたはASUS Tinker Board(またはS)に、SIMカードを差し込みます。SIMカードは、金属面を下向きにして取り付けます。

最後に、通信用USBケーブルでCANDY Pi LiteとラズパイまたはASUS Tinker Board(またはS)を接続します。

これで準備が整いました。それでは、ラズパイまたはASUS Tinker Board(またはS)に電源用USBケーブルを接続してラズパイを起動させましょう。

ラズパイまたはASUS Tinker Board(またはS)が起動したらログインをします。コマンドを入力できる環境を次のどちらかの方法で用意しましょう。

- デスクトップ画面（PIXEL環境）をお使いの場合は、ログインした後にスタートメニューのSystem Toolsから「LXTerminal」を選択して起動してください
- SSH環境をお使いになる場合は、SSHコマンドにてログインしてください

## ターミナルでの作業

ターミナルが開いたら、試しに以下のようなcURLコマンドを実行してみましょう。

```bash
$ curl -i -s -L --head https://www.candy-line.io/ | grep "200 OK"
```

下記のように`HTTP/1.1 200 OK`と出ていれば問題ありません。
```bash
HTTP/1.1 200 OK
```

続いてOSの状態が古い場合は、必要に応じて新しい状態に更新しましょう。
もしこのタイミングで更新したくなければ、この手順を飛ばしても構いません。
ただし、あまりにも古いOSであれば動作しない可能性もありますので、その場合は更新することを検討してください。

**注意：意図しないパケット消費を防ぐため、以下のコマンドを実行する前にモバイルネットワークに接続していないか確認しましょう。**

```bash
$ sudo apt-get upgrade -y
```
なお、この処理には、SDカードのクラス(読み書き速度)、更新するデータ量、あるいはネットワーク環境によりますが30分〜1時間以上かかることがあります。

それでは、GitHub上にあるスクリプトをダウンロードしてインストールします。

**注意：以下のコマンドは、プリインストールされているNode-REDを削除し、[CANDY RED](https://github.com/CANDY-LINE/candy-red)に置き換えます（Node-REDと同じ使い方をすることができますのでNode-REDの代わりとしてお使いいただけます）。Node.jsを更新するため、プリインストールされているNode-REDを残しておくことができないので削除しています。既存のフローをお持ちの場合は、[Node-REDからの移行方法](node-red-migration.md)を参照してください。**

### APN指定をしてセットアップ

以下のコマンドを実行すると（`git.io`もGitHubの管理するドメインの1つです）、接続先のAPNを指定してセットアップを開始します。なお、[`candy-pi-lite-service v1.8.0`](https://forums.candy-line.io/t/v1-8-0/90)以降からは、[有線LAN固定IP設定](/configuration/ether-static-ip.md)を特別な設定なくご利用頂けます。

`BOOT_APN`には、あらかじめ用意されているAPN設定を指定することができます。`BOOT_APN`を省略することもでき、その場合は、`soracom.io`として扱われます。

```bash
$ curl -sL https://git.io/v7bXx | sudo BOOT_APN=<apn名> bash
```
`<apn名>`には、現在[プリセットされたAPNの一覧](/configuration/apn-list.md)に記載された値を指定することができます。

例えば、IIJモバイル/タイプIのIPv4/IPv6接続を指定するときは、以下のように指定します。

```bash
$ curl -sL https://git.io/v7bXx | sudo BOOT_APN=iijmobile.biz-ipv4v6 bash
```

### デフォルトのAPNを指定してセットアップ

`BOOT_APN`を省略すると、デフォルトのAPNを指定した状態でセットアップします。

```bash
$ curl -sL https://git.io/v7bXx | sudo bash
```

### 指定したバージョンのcandy-pi-lite-serviceをセットアップ

また、candy-pi-lite-serviceの特定のバージョンを利用する場合は、以下のようにバージョンを指定することができます。なお、[CANDY RED](https://github.com/CANDY-LINE/candy-red)については、常に最新のバージョンのものだけを利用することができます。
```bash
$ VERSION=1.2.3 && \
  curl -sL https://raw.githubusercontent.com/CANDY-LINE/candy-pi-lite-service/${VERSION}/install.sh | \
  sudo bash
```

**注意：すでにcandy-pi-lite-serviceをインストールしている場合にインストールをしようとしてもインストールされません。エラーメッセージが出て、アンインストールするコマンドを実行するように促されます。このため、必ず一度アンインストールを行ってからインストールを行ってください。**

### セットアップコマンドの実施結果

実行すると以下のように表示されます。

    [INFO] Installing command lines to /opt/candy-line/candy-pi-lite/bin...
              :
              :
    [INFO] Installing CANDY RED...
              :
              :
    [INFO] candy-pi-lite service has been installed
    [ALERT] *** Please reboot the system (enter 'sudo reboot') ***

なおインストールは早ければ15分程度で終わりますが、状況によっては1~2時間以上かかる場合もありますので、処理が止まっているように見えても途中で中断をしないようにしてください。
インストールに失敗したときは、[インストールエラー](installation-errors.md)の説明を参照してください。

## 動作確認

インストールした後は、以下のコマンドを実行して再起動させましょう。

**注意：ソラコムのSIMをお使いの場合は、挿し込んでいるSIMが「使用中」になっているかご確認ください。「休止中」の場合は、携帯電話ネットワークに接続できず、オレンジのLEDが点滅しません。**

```bash
$ sudo reboot
```

再起動後しばらくすると、CANDY Pi LiteのオレンジのLEDが点滅します。これはモデムが起動していることを表しています。

CANDY Pi LiteのLEDが点滅していれば、セットアップは完了です！

なお、接続方法によって次のようにLEDの明滅パターンが異なります。詳細は、[LED設定]((/configuration/led.md))をご覧ください。

[CANDY REDへのブラウザー接続](browsing-candy-red.md)のページを参照して、[CANDY RED](https://github.com/CANDY-LINE/candy-red)を動かしてみましょう。
あるいは、すでにラズパイまたはASUS Tinker Board(またはS)で動作するアプリケーションをお持ちの場合は、動かしてみましょう。

もし圏外だったり、アンテナが接続されていなかったりした場合は、モデムは起動できません。LEDの表示はオレンジ色の1つのみ点灯します。
うまく動かない時は[トラブルシューティング](/troubleshooting.md)のページにモデムが起動しない場合の対処策をまとめていますので、ご確認ください。

また、既定の設定では、ソラコムのAPN設定が反映されます。このため、お使いのSIMカードがソラコム以外のものである場合は、[APN変更方法](/configuration/apn.md)に記載の方法で変更する必要があります。
