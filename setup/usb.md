<!-- toc -->

# USB接続を利用する場合の準備

![CANDY Pi Lite with USB Extension Board](/assets/candy-pi-lite-with-usb.png)

本章では、このようにUSB拡張ボードを **取り付けた状態で** 3G/LTE通信を行うためのセットアップ方法を説明します。
USB拡張ボードを使わない場合は、[セットアップの仕方（低速通信）](uart.md)をご覧ください。

## 用意するもの

USB接続でCANDY Pi Liteをご利用になる場合は、以下のものを用意しましょう。なお、ケーブル類やSIMカード、工具類はCANDY Pi Liteに付属しませんので、利用者の方がご用意ください。

- 組み立て済みのCANDY Pi Lite（アンテナも取り付けてください）
- 電源用USBケーブル、または5VACアダプター（内径：φ2.1mm、外径：φ5.5mm）
- 通信用USBケーブル
- LANケーブル
- nano（ナノ）サイズのSIMカード
- 精密ドライバー(+, #1)

*ご注意）ラズパイまたはASUS Tinker Board(またはS)に直接ログインする場合は、上記のほかディスプレイ、HDMIケーブル、USBキーボード、それにUSBマウスが必要です。*

### 電源用USBケーブル、または5VACアダプター

ラズパイまたはASUS Tinker Board(またはS)へ電源を供給するために、電源用USB2.0対応のタイプAオス-マイクロタイプBオスケーブルを利用します。5VのACアダプターをご利用の場合は、ACアダプターが対応する電流容量に注意しましょう。例えば、HDDやSSDなどの外部のUSBデバイスを取り付ける場合は、それらの電力も考慮した容量が必要です。電流容量が足りないACアダプターで運用すると、電力不足によってラズパイは停止または再起動を行うため、安定稼働を行うことができなくなってしまいます。

短時間での利用や開発時には、USBケーブルで電源供給することも可能です。このUSBケーブルは、パソコンとスマートフォンを繋げるようなタイプのケーブルを利用できます。
ただし、その場合でも電力不足を確認できた場合は、電流容量の大きいACアダプターの利用に切り替えてください。

**⚠️ DCジャックは、最大4Aまで対応しています。それより大きいACアダプターを利用しないようにしてください。**

### 通信用USBケーブル

通信用のUSBケーブルは、電源用のUSBケーブルと同じタイプのものを利用できます。ただし、長いケーブルである必要はないので、例えば、千石電商で入手できる[USB2.0ケーブル(A-microB) 0.15m](https://www.sengoku.co.jp/mod/sgk_cart/detail.php?code=EEHD-4X7E)や、秋月電子通商で入手できる[ＵＳＢケーブル　Ａオス－マイクロＢオス　０．１５ｍ　Ａ](http://akizukidenshi.com/catalog/g/gC-09312/)などを利用することができます。

CANDY Pi LiteをラズパイまたはASUS Tinker Board(またはS)と組み合わせて3G/LTE通信を行う場合は、通信用USBケーブルを経由して電源供給を行うことはありません。このため、通信用USB接続のケーブルには大容量の電流を想定したケーブルを用いる必要はありません。

### LANケーブル

LANケーブルは、ラズパイまたはASUS Tinker Board(またはS)からインターネットへ接続したり、パソコンから接続できるようにするために使用するものです。
Wi-Fiの接続で代用することも可能です。ただし、本書ではラズパイでのWi-Fi設定方法は記載しませんので、関連するサイトや書籍をご覧の上ご利用ください。

### nano(ナノ)サイズのSIMカード

CANDY Pi Liteには、nano（ナノ）サイズのSIMカードを挿しこみます。金属面を下にして以下のような方向に挿し込んでください。

![How to insert a SIM card](/assets/candy-pi-lite-sim-direction.jpg)

### 精密ドライバー(+, #1)

USB拡張ボードをCANDY Pi Liteに取り付けるためには、#1のプラス(+)の精密ドライバーが必要です。
ネジで固定しない場合、コネクター部分が破損したり、接続が不安定になったりしますので、必ずネジで固定するようにしてください。

### USB拡張ボードの取り付け

「[CANDY Pi Lite 3Gモデルの組み立て](assemble-3g.md)」、「[CANDY Pi Lite LTEモデルの組み立て](assemble-lte.md)」または「[CANDY Pi Lite+の組み立て](assemble-plus.md)」の図解をご覧になり、四角で囲んだ番号1から6を参照してください。

### USB接続の確認

USBが正しく接続されているか確認する場合は、USB拡張ボードの取り付けてUSBケーブルをラズパイまたはASUS Tinker Board(またはS)に差し込んでから、電源を入れてコマンドライン（ターミナル）にて、以下のコマンドを実行してください。

```
$ lsusb
Bus 001 Device 021: ID 05c6:9003 Qualcomm, Inc. Quectel UC20
Bus 001 Device 003: ID 0424:ec00 Standard Microsystems Corp. SMSC9512/9514 Fast Ethernet Adapter
Bus 001 Device 002: ID 0424:9514 Standard Microsystems Corp. SMC9514 Hub
Bus 001 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub
```

ここで、IDの箇所をご覧いただき、数字とアルファベットの組み合わせが以下のどれかに当てはまるものがあれば、USBで接続ができている状態となります。なお、この例ではIDの数字とアルファベットの左隣に`Qualcomm, Inc. Quectel UC20`と出ていますが、モジュールによっては何も表示されない場合や文字列が異なる可能性もありますので、IDの値でご判断ください。

| 機種               | ID         |
| ----------------- | ----------- |
| CANDY Pi Lite 3G  | `05c6:9003` |
| CANDY Pi Lite LTE | `2c7c:0121` |
| CANDY Pi Lite+    | `2c7c:0125` |

# 次のステップ

準備ができましたら、「[セットアップの開始](terminal.md)」をご覧ください。
