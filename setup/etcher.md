<!-- toc -->

# OSイメージファイルを利用したセットアップ

** 👉 すでにお持ちのSDカードにインストールする場合は[こちら](/setup/terminal.md)をご覧ください **

## OSイメージのダウンロード

まずは、CANDY Pi Lite向けセットアップ済みのRaspbian OSイメージをダウンロードしましょう。OSイメージは、以下のページから数字がもっとも大きい最新のバージョンを探してダウンロードしましょう。

```
https://forums.candy-line.io/tags/os
```

以下の画面の時点では、「1.3.0」が最新となりますので、その項目をクリックします。

_⚠️実際の画面では「1.3.0」よりも新しい場合がありますので、その場合は最新のバージョンをクリックしてください_
![etcher-01.png](/assets/etcher-01.png)

すると、以下のようなページが出現します。
![etcher-02.png](/assets/etcher-02.png)

四角で囲ったところから、「日本語版イメージファイル」または「US英語版イメージファイル」をダウンロードすることができます。

光回線の環境であれば、通常5分〜15分程度でダウンロード可能です。また、上記記載にもありますが、[ブログ記事](https://candy-line.tumblr.com/post/167761781228/candy-pi-lite-os-image-etcher)上でもOSイメージの準備方法を記載していますので、より細かいOSイメージの利用方法についてはブログも参照してください。

## マイクロSDカードの準備

OSイメージをマイクロSDに書き込むためには、[Etcher](https://etcher.io)を利用します。Etcherは、Windows、macそれにLinuxデスクトップで利用することができます。

こちらのサイトでソフトウェアをダウンロードしてインストールしましょう。
![etcher-03.png](/assets/etcher-03.png)

ダウンロードとインストールができたら、Etcherを起動しましょう。

![etcher-04.png](/assets/etcher-04.png)
最初に、イメージファイルを選択します。ダウンロードしたイメージファイルを「Select image」をクリックして選択します。 マイクロSDカードをパソコンに取り付けると、「Flash!」を押せるようになります。

![etcher-05.png](/assets/etcher-05.png)
書き込みには、5分程度かかります。また、書き込みの際に、特権ユーザーのパスワードが聞か れる場合がありますので、その場合は、パスワードの入力を行います。 書き込みが終わったら、次のステップに進みます。

## 動作確認

書き込みが終わったら、ラズパイにマイクロSDカードを差し込んで起動してみましょう。

**注意：ソラコムのSIMをお使いの場合は、挿し込んでいるSIMが「使用中」になっているかご確認ください。「休止中」の場合は、携帯電話ネットワークに接続できず、オレンジのLEDが点滅しません。**

電源を入れてからしばらくすると、CANDY Pi LiteのオレンジのLEDが点滅します。これはモデムが起動していることを表しています。

CANDY Pi LiteのLEDが点滅していれば、セットアップは成功です！

[CANDY REDへのブラウザー接続](browsing-candy-red.md)のページを参照して、[CANDY RED](https://github.com/CANDY-LINE/candy-red)を動かしてみましょう。
あるいは、すでにラズパイで動作するアプリケーションをお持ちの場合は、動かしてみましょう。

もし圏外だったり、アンテナが接続されていなかったりした場合は、モデムは起動できません。LEDの表示はオレンジ色の1つのみ点灯します。
うまく動かない時は[トラブルシューティング](/troubleshooting.md)のページにモデムが起動しない場合の対処策をまとめていますので、ご確認ください。

また、既定の設定では、ソラコムのAPN設定が反映されます。このため、お使いのSIMカードがソラコム以外のものである場合は、[APN変更方法](/configuration/apn.md)に記載の方法で変更する必要があります。

## SSHについて

OSイメージを書き込んだ初期状態では、**SSHが有効になっていません**。これは、OSイメージに書き込まれたパスワードがラズパイのデフォルト情報と同じであるため、SSHを有効にしてしまうと思わぬトラブルが発生してしまうためです。このため、SSHをご利用になるためには、通常のRaspbianと同様に、マイクロSDカードの`boot`フォルダーにファイル名`ssh`のファイルを作成してからラズパイを起動してください。ファイルの中身は無関係ですので、空のデータでもダミーのデータでも構いません。