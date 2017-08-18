<!-- toc -->

# candy-pi-lite サービスの再起動

candy-pi-lite サービスの再起動のため、停止と起動を一度に行う場合は、ターミナルから以下のコマンドを実行してください。

```bash
$ sudo systemctl restart candy-pi-lite
```

起動後、動作状態を確認するには、以下のコマンドを実行してください。

```bash
$ sudo systemctl status candy-pi-lite
```

実行すると、以下のように表示されます。3行目に`Active: active (running)`となっていれば、動作中です。

```
● candy-pi-lite.service - CANDY Pi Lite Service, version:1.0.0
   Loaded: loaded (/lib/systemd/system/candy-pi-lite.service; enabled)
   Active: active (running) since Thu 2017-08-17 08:17:05 UTC; 19h ago
 Main PID: 771 (bash)
   CGroup: /system.slice/candy-pi-lite.service
           ├─ 771 bash /opt/candy-line/candy-pi-lite/start_systemd.sh
           └─1918 python /opt/candy-line/candy-pi-lite/server_main.py /dev/ttySC1 460800 ppp0

Aug 17 09:10:55 shinycandypi pppd[1457]: Using interface ppp0
Aug 17 09:10:55 shinycandypi pppd[1457]: Connect: ppp0 <--> /dev/ttySC1
Aug 17 09:10:56 shinycandypi pppd[1457]: CHAP authentication succeeded
Aug 17 09:10:56 shinycandypi pppd[1457]: CHAP authentication succeeded
Aug 17 09:11:26 shinycandypi pppd[1457]: IPCP: timeout sending Config-Requests
Aug 17 09:11:32 shinycandypi pppd[1457]: Connection terminated.
Aug 17 09:11:32 shinycandypi start_systemd.sh[771]: Device "ppp0" does not exist.
Aug 17 09:11:32 shinycandypi pppd[1457]: Serial link disconnected.
Aug 17 09:11:33 shinycandypi server_main.<module>[1918]: serial_port:/dev/ttySC1 (460800 bps), nic:ppp0
Aug 17 09:11:33 shinycandypi server_main.__init__[1918]: RESTART_SCHEDULE_CRON=>[] is ignored
```
