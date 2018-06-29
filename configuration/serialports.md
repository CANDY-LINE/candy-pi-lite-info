## 利用可能なシリアルポートについて

candy-pi-lite-serviceをインストールすると、以下のシリアルポートを使用可能です。

モバイル通信モジュールのシリアルポートについては、ご利用の機種や接続方法（USB接続か、SPI/UART接続か）によって、シリアルポートの名称が変わりますのでご注意ください。

その他のデバイスのシリアルポートは、対応製品をUSBに差し込んだ際に有効になります。

また、シリアルポートの設定は多くのコマンドで初期設定となる以下の設定となります。

- データビット: 8
- パリティ: なし
- ストップビット: 1

### モバイル通信モジュールのシリアルポート

通信モジュールに関係するシリアルポートは以下の通りです。ボーレートが複数記載されているところは、ATコマンドの反応がない時に複数お試しください。

| 機種               | 接続方法           | シリアルポート名       | ボーレート(baud)     | 役割              |
| ----------------- | ----------------- | ----------------- -- | ------------------ | ---------------- |
| CANDY Pi Lite 3G  | GPIOピン(SPI/UART) | /dev/ttySC1         | 460800 または 115200 | ATコマンド、あるいはPPP接続（どちらか片方のみ） |
| CANDY Pi Lite 3G  | USB               | /dev/QWS.UC20.AT    |  115200             | ATコマンド |
| CANDY Pi Lite 3G  | USB               | /dev/QWS.UC20.MODEM |  115200             | PPP通信   |
| CANDY Pi Lite 3G  | USB               | /dev/QWS.UC20.NMEA  |    9600             | NMEA出力  |
| CANDY Pi Lite LTE | GPIOピン(SPI/UART) | /dev/ttySC1         | 460800 または 115200 | ATコマンド、あるいはPPP接続（どちらか片方のみ） |
| CANDY Pi Lite LTE | USB               | /dev/QWS.EC21.AT    | 115200              | ATコマンド |
| CANDY Pi Lite LTE | USB               | /dev/QWS.EC21.MODEM | 115200              | PPP通信   |
| CANDY Pi Lite+    | GPIOピン(SPI/UART) | /dev/ttySC1         | 460800 または 115200 | ATコマンド、あるいはPPP接続（どちらか片方のみ） |
| CANDY Pi Lite+   | USB                | /dev/QWS.EC25.AT    |  115200              | ATコマンド |
| CANDY Pi Lite+   | USB                | /dev/QWS.EC25.MODEM |  115200              | PPP通信   |
| CANDY Pi Lite+   | USB                | /dev/QWS.EC25.NMEA  |    9600              | NMEA出力  |

### その他のデバイスのシリアルポート

以下のシリアルポートは、CANDY Pi Lite/+の機種に関係なく、関係するデバイスが接続された時に有効となる名称です。

| デバイス                  | シリアルポート名 | ボーレート(baud) | 役割 |
| ------------------------ | ------------- | -------------- |
| [EnOcean USB 400J Gateway](https://www.enocean.com/jp/enocean_modules_928mhz/usb-400j/) | /dev/enocean | 57600 | EnOcean通信 |
| [SmartMesh IP USB Network Manager, 100 Mote Capacity (DC2274A-A)](http://www.analog.com/en/design-center/evaluation-hardware-and-software/evaluation-boards-kits/dc2274a-a.html#eb-documentation) | DC2274A-A.CLI | 115200 | CLIインタフェース |
| [SmartMesh IP USB Network Manager, 100 Mote Capacity (DC2274A-A)](http://www.analog.com/en/design-center/evaluation-hardware-and-software/evaluation-boards-kits/dc2274a-a.html#eb-documentation) | DC2274A-A.API | 115200 | APIインタフェース |
| [SmartMesh IP USB Access Point Mote (DC2274A-B)](http://www.analog.com/en/design-center/evaluation-hardware-and-software/evaluation-boards-kits/dc2274a-b.html) | DC2274A-B.CLI | 115200 | CLIインタフェース |
| [SmartMesh IP USB Access Point Mote (DC2274A-B)](http://www.analog.com/en/design-center/evaluation-hardware-and-software/evaluation-boards-kits/dc2274a-b.html) | DC2274A-B.API | 115200 | APIインタフェース |
