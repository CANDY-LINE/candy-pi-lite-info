<!-- toc -->

# LED設定

既定の設定では、モデムが動作し、携帯電話のネットワークに接続している間はCANDY Pi LiteのLEDが点滅します。また、その時間間隔は0.4秒となっています。

## LED点滅時間の指定

LED点滅に関する時間の設定は、インストール後に`/opt/candy-line/candy-pi-lite/environment`にある以下の箇所に定義されています。

```
# 1 for enabling LED blinking, 0 for disabling it
BLINKY=1
# Blinking interval in seconds, > 0 and <= 60
BLINKY_INTERVAL_SEC=0.4
```

`BLINKY`を0にすると、点滅をなくすことができます。ただし、常時点灯させることはできません。

`BLINKY_INTERVAL_SEC`には、点滅の時間間隔を秒で指定します。小数点を使うことができます。0より大きく、60以下の値を設定します。

点滅のパターンは以下の通りです。

- 点滅を2回素早く行い、その後消灯が少し長く続きます。これを繰り返します


これらの設定を変更した場合は、[candy-pi-lite サービスを再起動](/service/restart.md)するか、ラズパイを再起動する必要があります。
