# CANDY Pi Lite/CANDY Pi Lite+ 利用ガイド

![CANDY Pi Lite with Raspberry Pi](/assets/candy-pi-lite-birdview-small.png)

CANDY Pi Lite及びCANDY Pi Lite+（以降、CANDY Pi Lite/+と表記します）は、Raspberry Pi（ラズベリーパイ、以下ラズパイ）や、ASUS Tinker Board(またはS)に取り付けて使用する3G/4G LTE通信ボードです。

CANDY Pi Lite 3Gモデルでは、3G回線をご利用頂けます（日本国外では2G及び3G回線をご利用いただけます）。CANDY Pi Lite LTEモデルでは、4G LTE回線をご利用頂けます。CANDY Pi Lite LTE-Mモデルでは、LTE-M回線、NB-IoT回線をご利用頂けます（日本国外では2G回線もご利用いただけます）。

CANDY Pi Lite+ Dモデルでは、NTTドコモの3G/4G LTE回線をご利用いただけます。CANDY Pi Lite+ Kモデルでは、au/KDDIの4G LTE回線とNTTドコモの3G/4G LTE回線をご利用いただけます。CANDY Pi Lite+ Sモデルでは、Softbankの3G/4G LTE回線をご利用いただけます。

CANDY Pi Lite+（マルチキャリア版）モデルでは、NTTドコモの3G/4G LTE回線、au/KDDIの4G LTE回線、それにSoftbankの3G/4G LTE回線をご利用いただけます。

本書では、CANDY Pi Lite/+の利用方法について、組立方法、利用開始までのセットアップ方法、また製品の外寸などのハードウェア情報を解説します。CANDY Pi Lite/+の活用方法やチュートリアルについては、[CANDY LINE Blog](https://candy-line.com/blog/) をご覧ください。

CANDY Pi Lite/+とそのサービスソフトウェア(candy-pi-lite)は、標準でPPPと呼ばれる方式で携帯電話ネットワークへ接続します。CANDY Pi Lite/+に搭載している通信モジュールは、Qualcomm Modem Interface(QMI)に対応しているため、USB接続で利用された場合は、QMI WWANを利用して通信を行うことも仕様上は可能です。しかし、今のところcandy-pi-lite サービスではQMI WWANに対応していません。

# 本書について

本書の内容は、随時加筆修正が行われます。最終更新日をご確認ください。

# 法律とライセンス

本書の著作権は、株式会社 CANDY LINEが保有しています。
本書の文章や写真等イメージデータの内容は、[CC-BY-NC-SA 4.0](https://creativecommons.org/licenses/by-nc-sa/4.0/)ライセンスの下で公開されます。

- 「CANDY Pi」、「CANDY LINE」は、株式会社 CANDY LINEの商標または登録商標です。
- 「Raspberry Pi」はRaspberry Pi財団の登録商標です。
- 「ASUS」は、ASUSTek Computerの登録商標です。
- 「Bluetooth」は、Bluetooth SIG,Inc.の登録商標です。
- 「EnOcean」は、EnOcean GmbHの登録商標です。
- その他の名称は、それぞれの所有者の商標または登録商標です。

その他、本書に記載されている製品名や会社名は、各企業の登録商標あるいは商標です。本文中では、「™」「®」マークが明記されていないことがあります。

# CANDY Pi Lite/+の使用について

⚠️CANDY Pi Lite/+の使用については、以下の点を注意してください。

1. **CANDY Pi Lite/+を水に濡らしたり、湿度の高いところで利用したり、あるいはまた結露が発生するような状況で利用しないようにしてください。**
1. **CANDY Pi Lite/+のDCジャックは、最大4Aまで対応しています。それより大きい電流容量のACアダプターを利用しないようにしてください。**
1. **CANDY Pi Lite/+のDCジャックは、初期ロットのASUS Tinker Board Sでは動作しないためお使いいただけません。2018年3月下旬以降に出荷されたASUS Tinker Board Sではご利用いただけます。**
1. **CANDY Pi Lite LTEモデルとCANDY Pi Lite+は、日本国内専用です。日本国外では利用してはいけません。**
1. **CANDY LINE®がインターネットで公開している情報以外の3G/4G LTE通信モデムに関する情報については、[リファレンス](references.md)ページ記載のメーカー情報をご覧ください。**
