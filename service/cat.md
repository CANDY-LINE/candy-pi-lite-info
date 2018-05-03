<!-- toc -->

# candy-pi-lite サービスのログ

candy-pi-lite サービスのログは、`/var/log/syslog`に出力されています。candy-pi-lite サービスの情報だけを表示するには、ターミナルから以下のコマンドを実行してください。

```bash
$ sudo journalctl -f -u candy-pi-lite -o cat
```
