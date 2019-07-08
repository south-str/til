# PHP

## Unixtimeと日付の相互変換

Unixtimeへの変換は`strtotime`、日付への変換は`date`を使う。

```sh
php -r 'echo strtotime("2019-06-30") . "\n";'
# => 1561852800
php -r 'echo date("Y-m-d", 1561852800) . "\n";'
# => 2019-06-30
```

タイムゾーンなども考慮する場合は`DateTime`クラスか`DateTimeImmutable`を使う。

