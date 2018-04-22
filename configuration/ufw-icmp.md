
# ufwを利用してグローバルIP経由のPingを拒否する方法

OCN mobile oneなど一部のSIM回線をご利用の場合、グローバルIPが割当たる場合があります。また、固定IPを利用できるSIM回線をご利用の場合も同様です。その場合には、`ping`コマンドを拒否したいケースがあるかもしれません。

以下の手順に従って設定を行うと、`ping`コマンドの要求をファイヤーウォールで拒否することができます。

## IPv4

```
$ sudo vi /etc/ufw/before.rules
(下記の変更を適用)
$ sudo ufw disable; sudo ufw --force enable
```

### before.rulesファイルの変更内容

```
変更前（以下の箇所を探してください）:
-A ufw-before-input -p icmp --icmp-type echo-request -j ACCEPT

変更後（DROPの行を追加します）:
-A ufw-before-input -p icmp -i ppp0 --icmp-type echo-request -j DROP
-A ufw-before-input -p icmp --icmp-type echo-request -j ACCEPT
```

## IPv6

```
$ sudo vi /etc/ufw/before6.rules
(下記の変更を適用)
$ sudo ufw disable; sudo ufw --force enable
```

### before6.rulesファイルの変更内容

```
変更前（以下の箇所を探してください）:
-A ufw6-before-input -p icmpv6 --icmpv6-type echo-request -j ACCEPT

変更後（DROPの行を追加します）:
-A ufw6-before-input -p icmpv6 -i ppp0 --icmpv6-type echo-request -j DROP
-A ufw6-before-input -p icmpv6 --icmpv6-type echo-request -j ACCEPT
```
