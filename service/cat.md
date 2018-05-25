<!-- toc -->

# candy-pi-lite サービスのログ

candy-pi-lite サービスのログは、`/var/log/syslog`に出力されています。candy-pi-lite サービスの情報だけを表示するには、ターミナルから以下のコマンドを実行してください。

```bash
$ sudo journalctl -f -u candy-pi-lite -o cat
```

また、`-f`を取り除くと、カーソルキーでログ情報を遡ってみることができるようになります。

```bash
$ sudo journalctl -u candy-pi-lite -o cat
```

そのほか、他のログと混ざりますが`tail`コマンドで閲覧することも可能です。

```bash
$ tail -1000 /var/log/syslog  # 最新1000行を見る
$ tail -f /var/log/syslog     # 常に最新を表示し続ける
```
