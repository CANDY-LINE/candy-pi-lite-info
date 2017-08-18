# アンインストールの仕方

CANDY Pi Liteをセットアップした際にインストールされたソフトウェアは、以下の方法でアンインストールできます。

* [candy-pi-lite サービスのアンインストール](candy-pi-lite-service.md)
* [CANDY REDのアンインストール](candy-red.md)

ただし、以下の設定は上記の方法では元に戻されません。

1. `/boot/config.txt`に追加された設定。元に戻したいときは、`/boot/config.txt.bak`を`/boot/config.txt`置き換えてください。`/boot/config.txt`に適用された変更は失われますのでご注意ください。
1. `/boot/overlays/sc16is752-spi0-ce1.dtbo`ファイル。不要な場合は、手動で削除してください。
