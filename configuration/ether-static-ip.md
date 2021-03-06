<!-- toc -->

# 有線LAN固定IP(IPV4)自動設定機能

** 👉[`candy-pi-lite-service v1.4.0`](https://forums.candy-line.io/t/v1-4-0/38)以降で対応しています **


有線LAN接続で固定IPをラズパイに設定するには、通常ラズパイの中にある設定ファイルを変更しなければなりません。一度だけ変える分にはそれほど手間にはなりませんが、頻繁に変更する必要があったり環境が変わったりした場合に、ラズパイとネットワークをつなげてから変更しないといけないため、手間がかかります。

そのような手間を軽減するため、[CANDY Pi Lite向けソフトウェアをセットアップ](/setup/terminal.md)したラズパイでは、SDカードに固定IPの設定をお使いにパソコンから保存することによって固定IPを設定できる方法を提供しています。

**⚠️ご注意** この機能は、ラズパイの有線LANのみに対して有効です。無線LANには対応していません。

## 全体の手順

[CANDY Pi Lite向けソフトウェアをセットアップ](/setup/terminal.md)したラズパイに、固定IPを設定するには、以下の手順を実施します。

1. 固定IPの設定を決めて、その設定をJSONファイル形式で保存します
1. JSONファイルを、CANDY Pi Lite向けのセットアップしたラズパイのSDカードに保存します
1. そのSDカードを使って、ラズパイを起動します

もしすでに、`/etc/dhcpcd.conf`ファイルに固定IPを指定されている場合は、それらを削除してください。具体的には例えば、以下の指定が入っていると正しく設定されません。

- `interface enx001122aabbcc`（`enx001122aabbcc`の値はお使いのラズパイにより異なります）
- `static ip_address=`で始まる設定
- `static routers=`で始まる設定
- `static domain_name_servers=`で始まる設定

**⚠️ご注意** この手順は、Raspbian OSの標準ネットワークサービスである`dhcpcd`サービスを利用する前提で記載されています。言い換えれば、通常セットアップしたRaspbian OSをお使いの場合にご利用いただける手順です。一方で、以前のバージョンで使われていた`networking`サービスを利用する場合の手順については記載していません。

それでは、詳細を見ていきましょう。

## 固定IPの設定をファイルに保存します

まずは固定IPの設定を決めましょう。それは、オフィスや学校であらかじめ決められた値かもしれませんし、ご自身で決める値かもしれません。ここでは仮に、以下の値とします。

1. 有線LANに固定IPを設定する
1. 固定IPのアドレスは`192.168.137.200`とする
1. そのアドレスのサブネットマスク（ネットマスク）は`255.255.255.0`とする
1. デフォルトゲートウェイは`192.168.137.1`とする
1. DNSは`192.168.137.1`とする

これを以下のような形でJSON形式のファイルにします。

この作業は、SDカードにアクセス可能なパソコン（Windows、Mac、Linux）で行います。テキストエディターなどで以下のファイルを作成しましょう。

```
{
  "ip_address":"192.168.137.200/24",
  "routers":"192.168.137.1",
  "domain_name_servers":"192.168.137.1"
}
```

項目の意味は以下の通りです。

- `ip_address` ... IPアドレスと、ネットマスクを指定します。ネットマスクはスラッシュとともにビット表示の数値を指定します。どのように変換するかは、「[ネットマスク ビット指定計算](https://www.google.co.jp/#q=ネットマスク+ビット指定計算)」で検索してみてください。この例では、ネットマスクは`255.255.255.0`であるため、`24`と変換します
- `routers` ... デフォルトゲートウェイを指定します。特に定めていない場合は、空欄(`""`)にしましょう
- `domain_name_servers` ... DNSを指定します。特に定めていない場合は、空欄(`""`)にしましょう

**⚠️ご注意** 上記すべての項目を指定してください。対応する値がないときは空欄にしましょう。項目が足りていないと設定を行いません。

もし、`routers`と`domain_name_servers`に対応する値がないときは、以下のようになります。

```
{
  "ip_address":"192.168.137.200/24",
  "routers":"",
  "domain_name_servers":""
}
```

ファイル名は、`boot-ip.json`とします。このファイル名には、一定の名前付けルールがあります。ファイル名をつけるときは、以下のルールに合うものを名付けるようにしてください。

- `boot-ip.json` または
- `boot-ip.<任意の名前>.json`（例えば、`boot-ip.my-office.json` といった形です。名前には、半角アルファベット、半角数字、半角ハイフン`-`、半角アンダースコア`_`以外は使わないようにしましょう）

## ラズパイで使っているSDカードにファイルを保存

続いて、作成したファイルをCANDY Pi Lite向けのセットアップをしたラズパイのSDカードに保存しましょう。

まずは、そのSDカードをお使いのパソコンへ差し込んでください。SDカードスロットがない場合は、USBのSDカードアダプターなどをお使いください。

SDカードが認識されると、`boot`というフォルダーが見えるようになります。その場所に、作成したファイル（今回の例では、`boot-ip.json`）をコピーしましょう。

コピーを行ったら、お使いのOSごとに決められた方法でSDカードを取り出しましょう。

## ラズパイを起動

それでは、設定を保存したSDカードをラズパイにセットして、LANケーブルでラズパイとパソコンをつなぎましょう。正しくセットできていることを確認したら、ラズパイの電源を入れましょう。

1分ほどすると、ラズパイにアクセスできるようになります。

Windowsをお使いの方は、Tera Termやputtyなどで、`192.168.137.200`へSSHで入れることを確認してみてください。この時、パソコン側もIPアドレスを、`192.168.137.200`を除いた`192.168.137.1`から`192.168.137.254`の値を指定する必要があります。

macOSをお使いの方は、ターミナルを起動して、`ssh pi@192.168.137.200`を実行してみましょう。こちらもネットワーク設定で、パソコン側のアドレスを、`192.168.137.200`を除いた`192.168.137.1`から`192.168.137.254`の値を指定する必要があります。

## うまく設定されない時や元に戻したい時は

もしうまく設定できない時や設定を誤った時は、設定を元に戻すリセットを行うことができます。

リセットをするには、`boot`のフォルダーに`boot-ip-reset`と言う名前のファイルを作成してください。中身は空欄で構いません。何か入っていたとしても無視されます。

Windowsであれば、メモ帳などでファイルを作成してコピーしてください。macOSやLinux（ラズパイも含みます）であれば、ターミナルから、
```
sudo touch /boot/boot-ip-reset
```
を実行してください。

この`boot-ip-reset`という名前のファイルが`boot`フォルダーに存在していると、ラズパイが起動した時に元の設定（DHCPを使う設定）にリセットされます。
