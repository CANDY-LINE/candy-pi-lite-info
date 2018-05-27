<!-- toc -->

# candy-pi-lite サービスの停止

candy-pi-lite サービスを停止するには、ターミナルから以下のコマンドを実行してください。
このサービスを停止すると、携帯電話ネットワークへ接続されていた場合は、その接続を終了します。また、接続時に点滅していたLEDが消灯します。

**ご注意：このサービスを停止すると、`candy`コマンドを使うことはできませんのでご注意ください。**

```bash
$ sudo candy service stop
```

[`candy-pi-lite-service v5.0.0`](https://forums.candy-line.io/t/v5-0-0)より前のバージョンの場合は、以下のコマンドを実行してください。

```bash
$ sudo systemctl stop candy-pi-lite
```

停止後、動作状態を確認するには、以下のコマンドを実行してください。

```bash
$ sudo candy service status
```

[`candy-pi-lite-service v5.0.0`](https://forums.candy-line.io/t/v5-0-0)より前のバージョンの場合は、以下のコマンドを実行してください。

```bash
$ sudo systemctl status candy-pi-lite
```

実行すると、以下のように表示されます。3行目に`Active: inactive (dead)`となっていれば、停止中です。

```
● candy-pi-lite.service - CANDY Pi Lite Service, version:1.0.0
   Loaded: loaded (/lib/systemd/system/candy-pi-lite.service; enabled)
   Active: inactive (dead) since Fri 2017-08-18 03:50:43 UTC; 46s ago
  Process: 30983 ExecStop=/opt/candy-line/candy-pi-lite/stop_systemd.sh (code=exited, status=0/SUCCESS)
 Main PID: 771 (code=exited, status=0/SUCCESS)

Aug 17 09:11:26 shinycandypi pppd[1457]: IPCP: timeout sending Config-Requests
Aug 17 09:11:32 shinycandypi pppd[1457]: Connection terminated.
Aug 17 09:11:32 shinycandypi start_systemd.sh[771]: Device "ppp0" does not exist.
Aug 17 09:11:32 shinycandypi pppd[1457]: Serial link disconnected.
Aug 17 09:11:33 shinycandypi server_main.<module>[1918]: serial_port:/dev/ttySC1 (460800 bps), nic:ppp0
Aug 17 09:11:33 shinycandypi server_main.__init__[1918]: RESTART_SCHEDULE_CRON=>[] is ignored
Aug 18 03:50:41 shinycandypi systemd[1]: Stopping CANDY Pi Lite Service, version:1.0.0...
Aug 18 03:50:41 shinycandypi stop_systemd.sh[30983]: /usr/bin/poff: No pppd is running.  None stopped.
Aug 18 03:50:42 shinycandypi start_systemd.sh[771]: /opt/candy-line/candy-pi-lite/start_systemd.sh: line 164:  1918 Terminated ..._NAME}
Aug 18 03:50:43 shinycandypi systemd[1]: Stopped CANDY Pi Lite Service, version:1.0.0.
Hint: Some lines were ellipsized, use -l to show in full.
```
