<!-- toc -->

# IP到達確認監視

** 👉[`candy-pi-lite-service v6.0.0`](https://forums.candy-line.io/t/v6-0-0)以降で対応しています **

## 概要

CANDY Pi Liteが通信中に移動するなどして圏外となった場合、通信モジュールは通信ができなくなります。その後、再び圏内に戻ると自動的に一定時間後に通信は復旧します。しかし、通信圏外になったかどうかは外部のプログラムなどからはわかりにくく、また、通信圏外時に
IPレベルでネットワークの到達確認を行うことが可能です。初期設定ではOFFになっていますので、使用する場合は下記を参照して設定を有効にしてください。

基本的な動作としては、一定時間間隔で`ping`コマンドをあらかじめ指定されたIPアドレスに対して1回発行し、その結果として応答が来れば到達確認OKとしています。もし、`ping`コマンドの応答が来ない場合は、その状態が一定時間続くかどうかを確認し、一定時間以上不到達となれば、到達確認失敗とします。この時、`PPP_PING_RESTART_IF_OFFLINE`に`0`以外の値をセットしていると、candy-pi-liteサービスの再起動を行います。到達確認が成功している間は、状態ファイル`/opt/candy-line/candy-pi-lite/__ip_reachable`が存在し続けます。

## 監視設定

IP到達確認監視を有効にするためには、インストール後に`/opt/candy-line/candy-pi-lite/environment`の内容を変更します。

```
# Network testing request interval in PPP Modem-mode (<5: disabled)
PPP_PING_INTERVAL_SEC=0

# Network reachability test destination ip address and ip version
PPP_PING_TYPE=NONE
PPP_PING_DESTINATION=1.1.1.1
PPP_PING_IP_VERSION=4
PPP_PING_OFFLINE_THRESHOLD=30
PPP_PING_RESTART_IF_OFFLINE=0
```

まずは、`ping`コマンドの実行間隔を変更します。`PPP_PING_INTERVAL_SEC`に秒数を指定します。30秒の場合は30を、1時間の場合は3600のように秒単位の値を指定します。間隔を狭めるとすぐに不到達を検知できますが、一方でオンラインの状態ではその分多くのパケット通信を行いますので、検知の重要性とパケット通信量との関係性を考慮して設定値を決めましょう。なお、この値を5秒未満にすると機能が無効になります。5秒以上の値を指定してください。

続いて、`PPP_PING_TYPE`に`TEST`と指定します。`NONE`のままでは監視が有効になりません。

さらに`ping`コマンドの宛先アドレスを次の2つの変数で指定します。
- `PPP_PING_DESTINATION` ... インターネット回線に出る場合は初期設定「1.1.1.1」で問題ありません。閉域網を利用している場合は、そのネットワークで存在するIPアドレスを指定します。またそのIPアドレスのホストは、`ping`の応答を返せる設定になっている必要があります。なお、この宛先にはIPアドレスを指定してください。ホスト名を指定すると名前を解決するための余計なパケット通信が発生するためです。また、有線LANや無線LANでアクセス可能なIPアドレスを指定することはできません。モバイルネットワーク経由でアクセスできるIPアドレスを必ず指定してください。
- `PPP_PING_IP_VERSION` ... 上記のアドレスが、IPv4のネットワークのものであれば`4`を、IPv6ネットワークのものであれば`6`をそれぞれ指定します。

`PPP_PING_OFFLINE_THRESHOLD`には、どのくらいの間`ping`コマンドに失敗すると不到達とみなすかの基準の時間を秒で指定します。

`PPP_PING_RESTART_IF_OFFLINE`には、到達確認失敗時にサービスの再起動をする場合は、`1`を、そうでない場合は`0`を指定します。

```
PPP_PING_OFFLINE_THRESHOLD ≦ PPP_PING_INTERVAL_SEC + 5
```

のように設定すると、最初の1回目の`ping`に失敗すると直ちに到達確認失敗とみなされます。

上記の5秒は、`ping`のタイムアウト時間です。この秒数は固定値となっています。

設定例は以下の通りです。

```
# Network testing request interval in PPP Modem-mode (<5: disabled)
PPP_PING_INTERVAL_SEC=30

# Network reachability test destination ip address and ip version
PPP_PING_TYPE=TEST
PPP_PING_DESTINATION=1.1.1.1
PPP_PING_IP_VERSION=4
PPP_PING_OFFLINE_THRESHOLD=60
PPP_PING_RESTART_IF_OFFLINE=0
```

これらの設定を変更した場合は、[candy-pi-lite サービスを再起動](/service/restart.md)するか、ラズパイを再起動する必要があります。

## IP到達状態を外部のプログラムなどから知るには

IP到達状態を外部のプログラムなどから知るには、実際にプログラム内でI/Oエラー（ネットワークエラー）を検知するか、あるいは下記の方法でファイルの状態を確認することにより、あらかじめ状況を知ることも可能です。

IPレベルでネットワークの到達確認に成功した時は、以下の場所に空のファイルが作成されます。

```
/opt/candy-line/candy-pi-lite/__ip_reachable
```

もし、到達失敗と判定されると、上記のファイルは削除されます。
