# CADNY REDのアンインストール

以下のコマンドを実行すると、[CANDY RED](https://github.com/CANDY-LINE/candy-red)を削除することができます。
```bash
$ sudo npm uninstall -g --unsafe-perm candy-red
```

**ご注意：必ず`-g`と`--unsafe-perm`を指定してください**

実行すると以下のように表示されます。
```bash
[INFO] candy-red service has been uninstalled.
- abbrev@1.1.0 node_modules/candy-red/node_modules/abbrev
- addressparser@1.0.1 node_modules/candy-red/node_modules/addressparser
                  :
                (省略)
                  :
- node-red-dashboard@2.4.3 node_modules/candy-red/node_modules/node-red-dashboard
- node-red-node-serialport@0.4.4 node_modules/candy-red/node_modules/node-red-node-serialport
- ws@2.3.1 node_modules/candy-red/node_modules/ws
- candy-red@5.0.0 node_modules/candy-red
```

ただし、アンインストール実行後も`/opt/candy-red/.node-red`の内容は削除されず残されます。
また、再びインストールを行ったときは、`/opt/candy-red/.node-red/node_modules`の内容は削除されます。
