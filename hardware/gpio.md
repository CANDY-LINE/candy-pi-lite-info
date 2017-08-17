# GPIOピンマッピング

CANDY Pi Liteはラズパイ上の以下のGPIOピンを使用しています。

GPIOをお使いの場合は、下記以外のピンをご利用ください。

| RPi GPIO(40pins) | GPIO HW Pin#  |   UC20/EC21   | CANDY Pi Lite |
| ---------------- | ------------- | ------------- | ------------- |
|  20 (OUT)        |     PIN 38    |    PERESET    |     RESET     |
|  12 (OUT)        |     PIN 32    |   W_DISABLE   |       -       |
|  10 (SPI0_MOSI)  |     PIN 19    |       -       |       SI      |
|   9 (SPI0_MISO)  |     PIN 21    |       -       |       SO      |
|  11 (SPI0_SCLK)  |     PIN 23    |       -       |      SCLK     |
|   7 (SPI0_CE1)   |     PIN 26    |       -       |       CS      |
|  21 (IRQ)        |     PIN 40    |       -       |      IRQ      |
|       -          |       -       |   LED_WWAN    |  LED1 (GREEN) |
|   4 (OUT)        |     PIN  7    |       -       |  LED2 (ORANGE)|

## LED2（オレンジ）

candy-pi-liteの動作状況を表します。一定パターンで点滅を繰り返しているときは、携帯電話ネットワークに接続されています。消灯の場合は、携帯電話ネットワークへ接続できていません。

## PERST（リセット）

PERSTをlowに落とすと、3G/LTE通信モジュールとCANDY Pi Lite上のSC16IS75xのチップの両方をリセットすることができます。lowに落とす時間は、UC20/EC21の技術資料(Hardware Design)によれば、150~460msと決められていますが、概ね1秒程度でもリセット可能です。

candy-pi-liteサービスでは、サービス起動時にモデムのリセットを常に行なっていますので、通常の利用であれば利用者の方が明示的にリセットを行う必要はありません。

## W_DISABLE（無線OFF）

W_DISABLEピンをlowに落とすと、3G/LTE通信モジュールの無線動作を止めることができます。ただし、この操作をして無線を停止した場合、candy-pi-liteサービスが接続できないことを検出するまでおよそ2~3分かかります。

通常は、candy-pi-liteサービスの停止によって通信を停止するようにしてください。

なお、W_DISABLEピンをhighに設定し直したとしても、通信が自動的に復帰することはありません。明示的にcandy-pi-liteサービスを再起動してください。また、無線接続を再開する場合は、W_DISABLEピンをhighに設定し直す必要がありますが、candy-pi-liteサービスは自動的に再設定を行いますので、利用者の方がW_DISABLEピンをhighに戻す必要はありません。
