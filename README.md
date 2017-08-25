# CANDY Pi Lite 利用ガイド

![CANDY Pi Lite with Raspberry Pi](/assets/candy-pi-lite-birdview-small.png)

CANDY Pi Liteは、Raspberry Pi（ラズベリーパイ、以下ラズパイ）に取り付けて使用する3G/LTE通信ボードです。

3Gモデルでは、3G回線をご利用頂けます。LTEモデルでは、LTE回線をご利用頂けます。

本書では、CANDY Pi Liteの利用方法について、組立方法、利用開始までのセットアップ方法、また製品の外寸などのハードウェア情報を解説します。CANDY Pi Liteの活用方法やチュートリアルについては、[CANDY LINE Blog](http://candy-line.tumblr.com/candy-pi-lite) をご覧ください。

CANDY Pi Liteとそのサービスソフトウェア(candy-pi-lite)は、標準でPPPと呼ばれる方式で携帯電話ネットワークへ接続します。CANDY Pi Liteに搭載している通信モジュールは、Qualcomm Modem Interface(QMI)に対応しているため、USB接続で利用された場合は、QMI WWANを利用して通信を行うことも仕様上は可能です。しかし、今のところcandy-pi-lite サービスではQMI WWANに対応していません。

# 本書について

本書の内容は、随時加筆修正が行われます。最終更新日をご確認ください。本書をオンラインでご覧になっている場合、PDF/Mobi/ePub版のドキュメントを入手するには、[こちら](https://www.gitbook.com/book/candy-line/candy-pi-lite/details)からダウンロード可能です。

本書の著作権は、株式会社 CANDY LINEが保有しています。
本書の文章や写真等イメージデータの内容は、[CC-BY-NC-SA 4.0](https://creativecommons.org/licenses/by-nc-sa/4.0/)ライセンスの下で公開されます。

# CANDY Pi Liteの使用について

⚠️CANDY Pi Liteの使用については、以下の点を注意してください。

1. **CANDY Pi Liteを水に濡らしたり、湿度の高いところで利用したり、あるいはまた結露が発生するような状況で利用しないようにしてください。**
1. **CANDY Pi LiteのDCジャックは、最大4Aまで対応しています。それより大きい電流容量のACアダプターを利用しないようにしてください。**
1. **CANDY Pi LiteのEC21-J搭載型LTEモデルは、日本国内専用です。日本国外では利用してはいけません。**
1. **LTEモデル、3Gモデル共に、日本国内のau/KDDIネットワークやSoftbank系ネットワークには接続できません**
1. **CANDY LINEがインターネットで公開している情報以外の3G/LTE通信モデムに関する情報については、[リファレンス](references.md)ページ記載のメーカー情報をご覧ください。**
