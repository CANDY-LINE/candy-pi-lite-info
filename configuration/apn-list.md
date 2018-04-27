<!-- toc -->

# プリセットされたAPNの一覧

初期状態では、以下のキーワードを`/boot/apn`ファイルに指定することができます。APNの指定方法やプリセットAPNの追加・変更方法については、[APN設定](apn.md)をご覧ください。

- `soracom.io` ... ソラコム　IPv4ネットワーク(3G/LTE共通、主にSORACOM日本向けAir SIM向け)
- `soracom.io-docomo` ... ソラコム　IPv4ネットワーク NTTドコモネットワーク限定(3G/LTE共通、主にSORACOMグローバルAir SIM向け)
- `lte-d.ocn.ne.jp` ... OCNモバイルONE　IPv4ネットワーク(LTE専用)
- `3g-d-2.ocn.ne.jp` ... OCNモバイルONE　IPv4ネットワーク(3G専用)
- `iijmio.jp` ... IIJmio IPv4ネットワーク(3G/LTE共通)
- `iijmio.jp-ipv4v6` ... IIJmio IPv4/IPv6デュアルスタックネットワーク(3G/LTE共通)
- `iijmio.jp-ipv6` ... IIJmio IPv6ネットワーク(3G/LTE共通)
- `iijmobile.jp` ... IIJモバイル／タイプD IPv4ネットワーク(3G/LTE共通)
- `iijmobile.jp-ipv4v6` ... IIJモバイル／タイプD IPv4/IPv6デュアルスタックネットワーク(3G/LTE共通)
- `iijmobile.jp-ipv6` ... IIJモバイル／タイプD IPv6ネットワーク(3G/LTE共通)
- `iijmobile.biz` ... IIJモバイル／タイプI＜フルMVNO＞ IPv4ネットワーク(3G/LTE共通)
- `iijmobile.biz-ipv4v6` ... IIJモバイル／タイプI＜フルMVNO＞ IPv4/IPv6デュアルスタックネットワーク(3G/LTE共通)
- `iijmobile.biz-ipv6` ... IIJモバイル／タイプI＜フルMVNO＞ IPv6ネットワーク(3G/LTE共通)
- `internet4gd.gdsp` ... Vodafone Global Enterprise M2M IPv4ネットワーク(3G/LTE共通)
- `m2m4biz.softbank` ... Softbank IoT/M2M SIMカード IPv4ネットワーク(3G/LTE共通)
- `isp.docomoiot.net` ... docomo IoTスターターSIMカード IPv4ネットワーク(3G/LTE共通)

**⚠️ご注意）IIJのSIMカードでIPv6をご利用の場合は、「CANDY Pi Lite LTE」をご利用ください。[IIJのエンジニアによる公式blog「てくろぐ」記事内「IPv6が利用可能な条件」](http://techlog.iij.ad.jp/archives/411)に記載の通り、LTEに対応した端末のみ同社のIPv6はサポートされます。このため、「CANDY Pi Lite 3G」はこの条件に当てはまりませんので、当該機種ではIIJのIPv6をご利用いただけません。**

**⚠️ご注意）SORACOM Air SIMのグローバル向けSIMカードを日本国内でご利用の場合は「`soracom.io-docomo`」を推奨します。標準のAPN設定「`soracom.io`」をご利用の場合は、接続までに5分前後の時間がかかる場合があります。**
