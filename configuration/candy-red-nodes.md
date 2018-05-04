<!-- toc -->

# CANDY REDへのノード設定

CANDY REDへノードを追加したり、削除したりする方法を説明します。

## CANDY REDへコマンドラインから新しいノードを追加するには

ブラウザー経由でインストールするには、メニューの「≡」を押して、「Manage palette」を選択すると、専用のダイアログが表示されます。「Install」タブを選んでインストールしたいノードのパッケージ名を検索してから「Install」を押すとインストールができます。この際、`apt-get`などで別途ソフトウェアのインストールが必要な場合は、ノードのインストールに失敗します。あらかじめ、コマンドラインで`apt-get`などを使用して依存するソフトウェアをインストールしておく必要があります。

一方で、コマンドラインでノードをインストールすることも可能です。その場合は、以下のようにコマンドを入れてください。

```
sudo systemctl stop candy-pi-lite
sudo systemctl stop candy-red
cd /opt/candy-red/.node-red
sudo npm install --unsafe-perm ノードモジュール名
sudo systemctl start candy-red
sudo systemctl start candy-pi-lite
```

なお、`candy-red`のログを確認したいときは、次のコマンドもご利用ください。

```bash
$ sudo journalctl -f -u candy-red -o cat
```

ノードモジュールは、こちらから検索できるノードをご利用ください。「ノードモジュール名」には、`node-red-contrib-cache`など、タイトルで表示される文字列を指定します。

`candy-red`を停止してから、インストール後に起動しています。また、`candy-pi-lite`を停止していますが、これはモバイルネットワーク経由でインストールを行わないようにするための処置です。もし意図してモバイルネットワーク経由でインストールするときは、`candy-pi-lite`を停止させないようにしてください。

## ノードのインストールが成功したのかどうかを判断するには

`npm`コマンドを使用してインストールした時に、以下のようにメッセージが出ることがあります。

```
npm WARN optional SKIPPING OPTIONAL DEPENDENCY: xpc-connection@~0.1.4 (node_modules/node-red-contrib-generic-ble/node_modules/noble/node_modules/xpc-connection):
npm WARN notsup SKIPPING OPTIONAL DEPENDENCY: Unsupported platform for xpc-connection@0.1.4: wanted {"os":"darwin","arch":"any"} (current: {"os":"linux","arch":"arm"})
npm WARN node-red-project@0.0.1 No repository field.
npm WARN node-red-project@0.0.1 No license field.
npm WARN In opencv@6.0.0 replacing bundled version of node-pre-gyp with node-pre-gyp@0.6.39
pi@raspberrypi:/opt/candy-red/.node-red $
```

これらのように`npm WARN`で始まるメッセージだけの場合、エラーではありませんのでインストールは成功しています。エラーになるときは、次のように`npm ERR! `で始まるメッセージがたくさん表示されて終わります。

```
...
...
npm ERR!
npm ERR! Please try running this command again as root/Administrator.

npm ERR! Please include the following file with any support request:
npm ERR!     /opt/candy-red/.node-red/npm-debug.log
pi@raspberrypi:/opt/candy-red/.node-red $
```

このような場合は、正しくインストールできていませんので、エラーメッセージを参照して対応を行う必要があります。よくあるエラーとしては、`sudo`や`--unsafe-perm`がつけられていないことによる権限エラー、あるいは、`sudo apt-get`などで特別に追加でインストールすべきソフトウェアがある場合にそれが見つからないというエラーです。

## CANDY REDへコマンドラインからノードを削除するには

ブラウザー経由でインストールするには、メニューの「≡」を押して、「Manage palette」を選択すると、専用のダイアログが表示されます。「Nodes」タブにインストール済みのノードが出てきますので、削除したいノードを探して「remove」を押せば削除できます。このとき、削除したいノードをすでにフローとして使用している場合は、削除できません（「remove」が出てきません）のでご注意ください。

また、コマンドラインでノードをアンインストールする場合は、以下のようにコマンドを入れてください。

```
cd /opt/candy-red/.node-red
sudo npm uninstall --unsafe-perm ノードモジュール名
sudo systemctl restart candy-red
```

ノードモジュールは、こちらから検索できるノードをご利用ください。「ノードモジュール名」には、`node-red-contrib-cache`など、タイトルで表示される文字列を指定します。

## CANDY REDへコマンドラインで非公開のノードを追加するには

GitHubなどで公開されているノードを改変したり、ご利用者の方自身で開発されたノードを追加する場合は、以下のような方法があります。

1. `/opt/candy-red/.node-red/node_modules`ディレクトリーの下に追加するモジュールのファイルを置く
1. `/opt/candy-red/.node-red/node_modules`ディレクトリーの下に追加するモジュールのリンクを作る

どちらの方法も利用可能ですが、`/opt/candy-red/.node-red`のディレクトリーは、`root`ユーザーの所有になっています。このため、ファイルのコピーやリンクの作成時には必ず`sudo`を利用してください。
