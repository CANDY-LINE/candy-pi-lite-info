<!-- toc -->

# GPIOピンマッピング

CANDY Pi Lite/CANDY Pi Lite+は以下のGPIOピンを使用しています。

GPIOをお使いの場合は、下記以外のピンをご利用ください。

| GPIO HW Pin#  | RPi GPIO(40pins) | ASUS Tinker Board(またはS)      |   UC20/EC21   | CANDY Pi Lite |
| ------------- | ---------------- | ---------------------- | ------------- | ------------- |
|     PIN 38    |  20 (OUT)        |  187 (OUT, GP6A3)      |    PERESET    |     RESET     |
|     PIN 32    |  12 (OUT)        |  239 (OUT, GP7C7)      |   W_DISABLE   |       -       |
|     PIN 19    |  10 (SPI0_MOSI)  |  257 (SPI2TXD, GP8B1)  |       -       |       SI      |
|     PIN 21    |   9 (SPI0_MISO)  |  256 (SPI2RXD, GP8B0)  |       -       |       SO      |
|     PIN 23    |  11 (SPI0_SCLK)  |  254 (SPI2CLK, GP8A6)  |       -       |      SCLK     |
|     PIN 26    |   7 (SPI0_CE1)   |  251 (SPI2CSN1, GP8A3) |       -       |       CS      |
|     PIN 40    |  21 (IRQ)        |  188 (IRQ, GP6A4)      |       -       |      IRQ      |
|       -       |       -          |           -            |   LED_WWAN    |  LED1 (GREEN) |
|     PIN  7    |   4 (OUT)        |  17 (OUT, GP0C1)       |       -       |  LED2 (ORANGE)|

## SPI接続について

本製品は、ラズパイやASUS Tinker Boardの40ピンGPIOにあるSPIを使用しています。ラズパイでは、`SPI0`を、ATBでは`SPI2`を使用します。ラズパイでもASUS Tinker Boardでもチップセレクト1(`CE1`/`CS1`)を物理的に常に占有していますので、SPIをお使いになる場合は、チップセレクト0(`CE0`/`CS0`)のピンをご利用ください。`CE1`/`CS1`を利用することはできませんのでご注意ください。

Raspberry Pi B+以降で使用できる`SPI1`については、残念ながら本製品の使用するGPIOピンが一部重複しているため使用できません。

ASUS Tinker Boardの`SPI0`については、ピンが重複していないため利用可能です。

## LED2（オレンジ）

candy-pi-liteの動作状況を表します。一定パターンで点滅を繰り返しているときは、携帯電話ネットワークに接続されています。消灯の場合は、携帯電話ネットワークへ接続できていません。

## PERST（リセット）

PERSTをlowに落とすと、3G/LTE通信モジュールとCANDY Pi Lite上のSC16IS75xのチップの両方をリセットすることができます。lowに落とす時間は、UC20/EC21の技術資料(Hardware Design)によれば、150~460msと決められていますが、概ね1秒程度でもリセット可能です。

candy-pi-lite サービスでは、サービス起動時にモデムのリセットを常に行なっていますので、通常の利用であれば利用者の方が明示的にリセットを行う必要はありません。

## W_DISABLE（無線OFF）

W_DISABLEピンをlowに落とすと、3G/LTE通信モジュールの無線動作を止めることができます。ただし、この操作をして無線を停止した場合、candy-pi-lite サービスが接続できないことを検出するまでおよそ2~3分かかります。

通常は、candy-pi-lite サービスの停止によって通信を停止するようにしてください。

なお、W_DISABLEピンをhighに設定し直したとしても、通信が自動的に復帰することはありません。明示的に[candy-pi-lite サービスを再起動](/service/restart.md)してください。また、無線接続を再開する場合は、W_DISABLEピンをhighに設定し直す必要がありますが、candy-pi-lite サービスは自動的に再設定を行いますので、利用者の方がW_DISABLEピンをhighに戻す必要はありません。
