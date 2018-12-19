# RaspberryPi(Raspbian)でモバイルルーターとして使用する設定

**👉[`candy-pi-lite-service v4.0.0`](https://forums.candy-line.io/t/v4-0-0)以降で対応しています**

CANDY Pi Liteを「Raspbian（ラズビアン）」で動作させるとき、設定を変更するとルーターとして扱うことができるようになります。ここでは、有線LANまたは無線LANから接続したデバイスが、CANDY Pi Liteのモバイルネットワーク接続を利用できるようにするための設定を説明します。

**👉 CANDY Pi Lite専用のOSイメージ v3.0.0以降では、すでにソフトウェアがインストールされていますが、初期状態では無効になっています**

なお、こちらの手順は、raspberrypi.orgの[Wi-Fiのアクセスポイントを設定するための手順](https://www.raspberrypi.org/documentation/configuration/wireless/access-point.md)をベースに作成しています。しかし、その手順とは異なり、`iptables`を直接利用しません。代わりに`ufw`を設定します。`ufw`の設定の詳細は、[Gist kimus/9315140](https://gist.github.com/kimus/9315140)の方法をベースに記載しています。

以下の手順を途中で中断すると、有線LANや無線LANが意図通りに接続できなくなる場合があります。その場合は、シリアルコンソールで設定を変更するか、OSイメージを書き直して最初からやり直してください。

## 有線LAN・無線LAN共通の手続き

### 追加ソフトウェアのインストール

**👉 専用イメージ利用時はこのインストール作業は不要です**

ラズパイをルーターとして動作させるために、DHCPサーバーの機能を追加します。

なお、CANDY Pi Liteを接続してインターネットに接続している場合は必ず下記コマンドを停止してください。

```
$ sudo systemctl stop candy-pi-lite
$ sudo apt-get update
$ sudo apt-get install dnsmasq
```

`dnsmasq`の設定をしていないため、一旦サービスを停止します。

```
$ sudo systemctl stop dnsmasq
```

### `ufw`の設定変更

`ufw`の設定を変更してルーティングを行うようにします。

```
$ sudo nano /etc/default/ufw
```

ここで、`DEFAULT_FORWARD_POLICY`の値を以下のように変更します。

```
DEFAULT_FORWARD_POLICY="ACCEPT"
```

続いて、`ufw`のルールファイルを変更します。

```
$ sudo nano /etc/ufw/before.rules
```

ここで、`*filter`と書かれた先頭の方にある設定の **前** に、以下の行を追加します。

```
# NAT table rules
*nat
:POSTROUTING ACCEPT [0:0]

# Forward traffic through ppp0
-A POSTROUTING -o ppp0 -j MASQUERADE

# don't delete the 'COMMIT' line or these nat table rules won't
# be processed
COMMIT
```

最後の`COMMIT`まで追加してください。

### `sysctl.conf`の設定変更

ipv4/ipv6のパケットフォワードを有効にするために、`sysctl.conf`を変更します。

```
$ sudo nano /etc/sysctl.conf
```

初期状態では通常コメントアウトされているので、以下のように`net.ipv4.ip_forward=1`の行の先頭の`#`を外してください。

```
# Uncomment the next line to enable packet forwarding for IPv4
net.ipv4.ip_forward=1

# Uncomment the next line to enable packet forwarding for IPv6
#  Enabling this option disables Stateless Address Autoconfiguration
#  based on Router Advertisements for this host
#net.ipv6.conf.all.forwarding=1
```

これ以降は、有線LAN経由でラズパイに接続する場合と、無線LAN経由でラズパイに接続する場合とで設定方法が異なりますので、目的に応じて手順を進めてください。

## 有線LANを経由した接続の場合

### 固定IPの設定

こちらは、有線LAN経由でラズパイに搭載されたCANDY Pi Liteの通信を使用する方法の設定手順です。

まずは固定IPを`eth0`に割り当てます。

```
$ sudo nano /boot/boot-ip.json
```

として、以下の内容を書き込みます。

```
{
  "ip_address":"192.168.5.1/24",
  "interface":"eth0"
}
```

### DHCPサーバーの設定

続いて、DHCPの設定を行います。

既存の`dnsmasq`の設定をバックアップして、新しい設定を保存します。

```
$ sudo mv /etc/dnsmasq.conf /etc/dnsmasq.conf.orig  
$ sudo nano /etc/dnsmasq.conf
```

新しい設定には以下の内容を書き込みます。
```
interface=eth0
  dhcp-range=192.168.5.2,192.168.5.20,255.255.255.0,24h
```

### 再起動

再起動後に`dnsmasq`サービスが起動するように有効にします。

```
$ sudo systemctl enable dnsmasq
```

これで準備は整いました。ラズパイを再起動してください。CANDY Pi Liteがモバイルネットワークに接続したら、Ethernetケーブルで接続したコンピューターからインターネットへアクセスを試みてください。

## 無線LANを経由した接続の場合

### 追加ソフトウェアのインストール

**👉 専用イメージ利用時はこのインストール作業は不要です**

無線LANのアクセスポイントを作成するために`hostapd`をインストールします。

```
$ sudo apt-get install hostapd
```

`hostapd`の設定をしていないため、一旦サービスを停止します。

```
$ sudo systemctl stop hostapd
```

### 固定IPの設定

次に固定IPを`wlan0`に割り当てます。

```
$ sudo nano /boot/boot-ip.json
```

として、以下の内容を書き込みます。

```
{
  "ip_address":"192.168.4.1/24",
  "interface":"wlan0"
}
```

### DHCPサーバーの設定

続いて、DHCPの設定を行います。

既存の`dnsmasq`の設定をバックアップして、新しい設定を保存します。

```
$ sudo mv /etc/dnsmasq.conf /etc/dnsmasq.conf.orig  
$ sudo nano /etc/dnsmasq.conf
```

新しい設定には以下の内容を書き込みます。
```
interface=wlan0
  dhcp-range=192.168.4.2,192.168.4.20,255.255.255.0,24h
```

### Wi-Fiアクセスポイントの設定

新しいWi-Fiアクセスポイントの作成に必要な情報をファイルに書き込みます。

```
$ sudo nano /etc/hostapd/hostapd.conf
```

以下の設定は、WPA2のものです。SSIDやパスフレーズなどを必要に応じて変更してください。

```
interface=wlan0
driver=nl80211
ssid=SSID名をここに書く
hw_mode=g
channel=7
wmm_enabled=0
macaddr_acl=0
auth_algs=1
ignore_broadcast_ssid=0
wpa=2
wpa_passphrase=SSIDのパスワードをここに書く
wpa_key_mgmt=WPA-PSK
wpa_pairwise=TKIP
rsn_pairwise=CCMP
```

次にこのファイルを初期設定とするように変更します。

```
$ sudo nano /etc/default/hostapd
```

初期状態では、次のように設定されているところがあります。

```
#DAEMON_CONF=""
```

これを以下のように、`#`を取り除き、`""`の中にパスを追記します。このパスはそのまま変更せずにコピー＆ペースとしてご利用ください。

```
DAEMON_CONF="/etc/hostapd/hostapd.conf"
```

### 再起動

再起動後に`dnsmasq`サービスと`hostapd`サービスが起動するように有効にします。

```
$ sudo systemctl enable dnsmasq
$ sudo systemctl enable hostapd
```

これで準備は整いました。ラズパイを再起動してください。指定したSSIDが見えるようになったらアクセスポイントにつないでみましょう。アクセスポイントで接続できたら、接続したコンピューターからインターネットへアクセスを試みてください。
