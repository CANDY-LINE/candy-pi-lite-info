<!-- toc -->

# プリセットされたAPNの一覧

初期状態では、以下のキーワードを`/boot/apn`ファイルに指定することができます。APNの指定方法やプリセットAPNの追加・変更方法については、[APN設定](apn.md)をご覧ください。

- `soracom.io` ... [ソラコム](https://soracom.jp)　IPv4ネットワーク(3G/LTE共通、主にSORACOM日本向けAir SIM向け。plan-D、plan-K共通)
- `soracom.io-docomo` ... [ソラコム](https://soracom.jp)　IPv4ネットワーク NTTドコモネットワーク限定(3G/LTE共通、主にSORACOMグローバルAir SIM向け)
- `lte-d.ocn.ne.jp` ... [OCNモバイルONE](https://www.ntt.com/personal/services/mobile/one.html)　IPv4ネットワーク(LTE専用)
- `3g-d-2.ocn.ne.jp` ... [OCNモバイルONE](https://www.ntt.com/personal/services/mobile/one.html)　IPv4ネットワーク(3G専用)
- `iijmobile.biz` ... [IIJモバイル／タイプI](https://www.iij.ad.jp/biz/iijmobile/) **＜フルMVNO＞** IPv4ネットワーク(3G/LTE共通)
- `iijmobile.biz-ipv4v6` ... [IIJモバイル／タイプI](https://www.iij.ad.jp/biz/iijmobile/) **＜フルMVNO＞** IPv4/IPv6デュアルスタックネットワーク(3G/LTE共通)
- `iijmobile.biz-ipv6` ... [IIJモバイル／タイプI](https://www.iij.ad.jp/biz/iijmobile/) **＜フルMVNO＞** IPv6ネットワーク(3G/LTE共通)
- `iijmio.jp` ... [IIJmio／タイプD・タイプA](https://www.iijmio.jp) IPv4ネットワーク(3G/LTE共通)
- `iijmio.jp-ipv4v6` ... [IIJmio／タイプD・タイプA](https://www.iijmio.jp) IPv4/IPv6デュアルスタックネットワーク(3G/LTE共通)
- `iijmio.jp-ipv6` ... [IIJmio／タイプD・タイプA](https://www.iijmio.jp) IPv6ネットワーク(3G/LTE共通)
- `iijmobile.jp` ... [IIJモバイル／タイプD・タイプK](https://www.iij.ad.jp/biz/iijmobile-dk/) IPv4ネットワーク(3G/LTE共通)
- `iijmobile.jp-ipv4v6` ... [IIJモバイル／タイプD・タイプK](https://www.iij.ad.jp/biz/iijmobile-dk/) IPv4/IPv6デュアルスタックネットワーク(3G/LTE共通)
- `iijmobile.jp-ipv6` ... [IIJモバイル／タイプD・タイプK](https://www.iij.ad.jp/biz/iijmobile-dk/) IPv6ネットワーク(3G/LTE共通)
- `sd.iijmobile.jp` ... [IIJモバイル（下り最大150Mbpsの通信速度向け）／タイプD・タイプK](https://www.iij.ad.jp/biz/iijmobile-dk/) IPv4ネットワーク(3G/LTE共通)
- `internet4gd.gdsp` ... [Vodafone Global Enterprise M2M](https://www.vodafone.com/business/iot/japan/global-sim) IPv4ネットワーク(3G/LTE共通)
- `m2m4biz.softbank` ... [Softbank IoT/M2M SIMカード](https://www.softbank.jp/biz/iot/) IPv4ネットワーク(3G/LTE共通)
- `isp.docomoiot.net` ... [docomo IoTスターターSIMカード](https://www.nttdocomo.co.jp/biz/special/iot/) IPv4ネットワーク(3G/LTE共通)
- `ipsim.net` ... [固定IPアドレスSIM イプシム](https://ipsim.net)([Qiita解説記事](https://qiita.com/ipsim_net/items/9cccb64a5afcc03ec0f1))
- `rokemoba` ... [ロケットモバイル](https://rokemoba.com)([TwitterでのCANDY Pi Lite対応済みツイート](https://twitter.com/rokemoba/status/1039000912604278786))
- `au.au-net.ne.jp` ... [au/KDDI LTE NET for DATA](https://www.au.com/mobile/charge/internet-connection/ltenet-for-data/)
- `uqmobile.jp` ... [UQ mobile](https://www.uqwimax.jp/mobile/)

**⚠️ご注意）IIJのSIMカードでIPv6をご利用の場合は、「CANDY Pi Lite LTE」をご利用ください。[IIJのエンジニアによる公式blog「てくろぐ」記事内「IPv6が利用可能な条件」](http://techlog.iij.ad.jp/archives/411)に記載の通り、LTEに対応した端末のみ同社のIPv6はサポートされます。このため、「CANDY Pi Lite 3G」はこの条件に当てはまりませんので、当該機種ではIIJのIPv6をご利用いただけません。**

**⚠️ご注意）SORACOM Air SIMのグローバル向けSIMカードを日本国内でご利用の場合は「`soracom.io-docomo`」を推奨します。標準のAPN設定「`soracom.io`」をご利用の場合は、接続までに5分前後の時間がかかる場合があります。**

**⚠️ご注意）ソフトバンクネットワークを使用するSIMカードを利用するには、`CANDY Pi Lite+ S` が必要です。 **

**⚠️ご注意）au/KDDIネットワークを使用するSIMカードを利用するには、`CANDY Pi Lite+ K` が必要です。 **

**⚠️ご注意）docomoネットワークを使用するSIMカードを利用する場合は、`CANDY Pi Lite LTE`、`CANDY Pi Lite 3G`、`CANDY Pi Lite+ D`、あるいは `CANDY Pi Lite+ K` が必要です。 **
