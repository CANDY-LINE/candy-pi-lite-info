<!-- toc -->

# Node-REDからの移行方法

通常candy-pi-lite-serviceをインストールすると、プリインストールされているNode-REDはアンインストールされます。これは、[CANDY RED](https://github.com/CANDY-LINE/candy-red)をインストールするときに、プリインストールされているNode.jsも更新するためです。

**注意：RASPBIAN STRETCH LITEやTinker OSをお使いの場合には、もともとNode-REDは含まれておりません**

一見、Node-REDが使えなくなってしまうようですが、[CANDY RED](https://github.com/CANDY-LINE/candy-red)はNode-REDがベースとなっていますので、Node-REDの代わりとしてそのままお使いいただけます。また、GUIをお使いの場合、スタートメニューのProgrammingの項目からNode-REDを起動できなくなりますが、[CANDY RED](https://github.com/CANDY-LINE/candy-red)はOSが起動された時に自動的に開始されます。

このため、メニューから明示的にスタートを行う必要はありません。

しかし、Node-REDで作成されたフローや、追加されたノードをお持ちの場合は、CANDY REDでも使えるようにするため、データ移行の手順を実施する必要があります。

## フローの移行

フローの移行には2つの方法があります。一つは、ブラウザーでフローのインポート(Import)を行う方法、もう一つはコマンドラインで実行する方法です。ここでは、後者の方法を紹介します。

ラズパイにSSHでログインまたは、デスクトップ画面からLXTerminal（スタートメニューのSystem Toolsから選択できます）を起動し、以下のコマンドを実行してください。パスワードを聞かれたら、ラズパイのログインに使用したパスワードを入力してください。

    pi@raspberrypi: ~ $ sudo cp ~/.node-red/flows_${HOST_NAME}.json \
    /opt/candy-red/.node-red/flows_candy-red.json

(`pi@raspberrypi: ~ $`は入力する必要はありません)

このコマンドにより、Node-REDが作成したフローファイルをCANDY REDが利用するファイルの場所にコピーすることができます。

## ノードの移行

Node-REDにプリインストールされていないノードを追加していた場合、[CANDY RED](https://github.com/CANDY-LINE/candy-red)にも追加する必要があります。Node-REDで行った場合と同じように、npmコマンドを使います。違いは、コマンドを実行するディレクトリーと`sudo`と`--unsafe-perm`を用いることです。`--unsafe-perm`は、全てのノードで必要になるとは限りませんが、ノードの種類によってはファイルのコピーにおいてエラーとなる場合がありますので、指定するようにしてください。

以下では、node-red-contrib-slackを[CANDY RED](https://github.com/CANDY-LINE/candy-red)に追加する例を示します。

    pi@raspberrypi: ~ $ cd /opt/candy-red/.node-red
    pi@raspberrypi: /opt/candy-red/.node-red $ sudo npm install --unsafe-perm node-red-contrib-slack
    pi@raspberrypi: /opt/candy-red/.node-red $ sudo systemctl restart candy-red

インストールしたノードを有効にするために、サービスを起動しなおす必要があります。これを上記3行目で行っています。単純に再起動する方法でも問題ありません。

## CANDY REDでのノード追加について

今後CANDY REDで新しいノードを追加するときは、上記のように`/opt/candy-red/.node-red`ディレクトリーでインストールを行う必要があります。通常のドキュメントでは、Node-RED向けのディレクトリー`~/.node-red`で説明がありますので読み替えるようにお願いいたします。
