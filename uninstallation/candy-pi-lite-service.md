<!-- toc -->

# candy-pi-lite サービスのアンインストール

ホームディレクトリーに移りアンインストールのスクリプトを実施してください。
```bash
$ cd ~
$ sudo /opt/candy-line/candy-pi-lite/uninstall.sh
```
このコマンドでは、[CANDY RED](https://github.com/CANDY-LINE/candy-red)は削除されません。[CANDY RED](https://github.com/CANDY-LINE/candy-red)を削除する場合は、「[CANDY REDのアンインストール](candy-red.md)」をご覧ください。

実行すると以下のように表示されます。
```bash
$ cd ~
$ sudo /opt/candy-line/candy-pi-lite/uninstall.sh
Removed symlink /etc/systemd/system/multi-user.target.wants/candy-pi-lite.service.
[INFO] candy-pi-lite has been uninstalled
Uninstalling candy-board-qws:
  Successfully uninstalled candy-board-qws
Uninstalling candy-board-cli:
  Successfully uninstalled candy-board-cli
[ALERT] *** Please reboot the system! (enter 'sudo reboot') ***
```
