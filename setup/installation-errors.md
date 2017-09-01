<!-- toc -->

# インストールに失敗した時は

## `registry.npmjs.org`へ接続できない

環境によっては、インストール実施中に以下のようなメッセージで終了することがあります。

    npm ERR! network getaddrinfo ENOTFOUND registry.npmjs.org
    npm ERR! network This is most likely not a problem with npm itself
    npm ERR! network and is related to network connectivity.
    npm ERR! network In most cases you are behind a proxy or have bad network settings.
    npm ERR! network
    npm ERR! network If you are behind a proxy, please make sure that the
    npm ERR! network 'proxy' config is set properly.  See: 'npm help config'

    > candy-red@2.8.0 preuninstall /usr/lib/node_modules/candy-red
    > ./uninstall.sh

    ls: cannot access /usr/lib/node_modules/candy-red/services/start_*: No such file or directory

    [ERROR] The service candy-red isn't installed yet.

    npm ERR! Please include the following file with any support request:
    npm ERR!     /root/npm-debug.log
    [INFO] Installing system service ...
    Created symlink from /etc/systemd/system/multi-user.target.wants/ltepi2.service to /lib/systemd/system/ltepi2.service.
    [INFO] candy-pi-lite service has been installed
    [ALERT] *** Please reboot the system (enter 'sudo reboot') ***

このような場合は、ご利用のネットワーク環境にて一時的にインターネットへ接続できていない可能性があります。
その結果、[CANDY RED](https://github.com/CANDY-LINE/candy-red)のインストールには失敗しております。しかし、candy-pi-lite-serviceのサービス自体はインストールできています。

この場合は、[CANDY REDのインストール方法](CANDY REDのインストール方法.md)をご覧いただき、[CANDY RED](https://github.com/CANDY-LINE/candy-red)のインストールを再度行うようにしてください。

## SDカードイメージ不正

2017-07-05バージョンのRaspbianをインストールすると、`files list file for package 'qdbus' is missing final newline`というdpkgのエラーが出る事象がありました。この場合は、イメージの書き込みに失敗している可能性があります。もし、DDコマンドを利用されているときは、`conv=sync`を追加してイメージデータが全て書き込まれるようにしてください。

- 参考URL: https://www.raspberrypi.org/forums/viewtopic.php?t=187936&p=1184738
