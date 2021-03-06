<!-- toc -->

# 追加部品、交換部品

## USBケーブル

USB接続をご利用の場合、ご利用者の方にUSBケーブルをご用意いただく必要があります。USBケーブルは電源を供給する必要はないため、多くの場合コネクターの形状があっていれば現在流通するケーブルを利用可能です。仕様上はUSB2.0の規格を満たしていればそれ以外の要件はありません。

個人利用であれば、充電専用ではないものであれば100円ショップのものでも利用可能ですし、大量に使用する場合は、下記のような商品をご利用ください。

- [USBケーブル（秋月電子通商）](http://akizukidenshi.com/catalog/c/cusbcable/)
- [USBケーブル（せんごくネット通販）](https://www.sengoku.co.jp/mod/sgk_cart/search.php?cid=3684)

ご購入の際は、USBケーブルのコネクターの形状にご注意ください。

- USBタイプAオス・・・「Raspberry Pi Model A+/Model B+/Pi2/Pi3」「ASUS Tinker Board」側
- マイクロUSB(マイクロB)オス・・・「CANDY Pi Lite」「CANDY Pi Lite+」接続側（「なにつなぐ？」ボード側）、「Raspberry Pi Zero/W/WH」側

\* Raspberry Pi Zero/W/WH」をご利用の場合、希望のケーブルがないときは変換コネクターもご利用いただけます。

## アンテナとSMA-U.FL変換ケーブルセット

「CANDY Pi Lite 3G」、「CANDY Pi Lite LTE」、「CANDY Pi Lite+ D」、「CANDY Pi Lite+ S」、「CANDY Pi Lite+ K」に付属しているアンテナとケーブルは、ソラコム社のコンソールから購入が可能です。

- メーカー：Hanwool Technology
- 型名：HW-MULTI-GA-RSMA
- 紹介サイト：https://soracom.jp/products/module/

アカウントを作成してから（無料）、管理コンソールの画面を通じて購入が可能です。
購入方法の詳細については、「[お問い合わせ](https://soracom.jp/contact/)」ページより直接ソラコム社へお問い合わせください。

## SMA-U.FL変換ケーブル

通信モジュールとアンテナとを取り付ける同軸ケーブルには、SMAとU.FLコネクターの変換ケーブルを利用しています。
このケーブルはSMAの根元部分や、U.FLの根元部分は取り外しのタイミングで破損しやすいため、取り扱いにはご注意ください。

ケーブルの取り外しの際には、指だけで取り外すとコネクターの根元を破損しやすいため、先がL字型のピンセットのようなものを使って以下の写真のようにしっかり掴んでから垂直に引っ張るようにすると安全に取り外しができます。

![ケーブル取り外し](/assets/how-to-remove-cable.png)

なおもし以下の写真のように破損してしまった場合は、下記の商品にて代用可能です（SMAコネクターの部分がリバースタイプではないもの）。

![U.FL破損部分](/assets/broken-U.FL.jpg)

- [SMA-U.FL変換ケーブル 長さ約10cm(せんごくネット通販)](http://www.sengoku.co.jp/mod/sgk_cart/detail.php?code=2DC5-UHLE)
- [RS Pro, 同軸ケーブルアセンブリ 150mm(アールエスコンポーネンツ)）](http://jp.rs-online.com/web/p/coaxial-cable-assemblies/7942897/)

## GNSS/GPSアンテナ・ケーブル

「CANDY Pi Lite 3G」と「CANDY Pi Lite+」については、GNSSモジュールが搭載されています。このモジュールを使うためには、専用のアンテナをご利用ください。付属のアンテナでも利用可能ですがケーブル長がほぼないため、常にラズパイを屋外か屋外近くに配置する必要があり実用的ではありません。

SMAコネクター接続のGNSS/GPSアンテナをご利用いただくとケーブルの取り回しがしやすく便利です。
なお、同軸ケーブルについては、付属品では足りない場合は上記SMAケーブルをご利用ください。

## DCジャック用ACアダプター

「CANDY Pi Lite 3G」、「CANDY Pi Lite LTE」や「CANDY Pi Lite+」に搭載されているDCジャックは、以下の規格に合致したACアダプターを利用することが可能です。

- 出力電圧：5V
- 出力電流：3Aまたは4A（Raspbrry PiやASUS Tinker Boardに取り付ける機器も加味してご検討ください）
- プラグ形状：DCプラグ・ジャック
- プラグ寸法：内径：φ2.1mm、外径：φ5.5mm
- 極性：センタープラス
