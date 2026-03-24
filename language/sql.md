# SQL

主にmysqlを扱う。

## unixtimestampから日付形式への変更

```
SELECT FROM_UNIXTIME(column)
FROM table
;
```

## 変数に格納した値をIN句で使う

仕様上使えないので代わりに`FIND_IN_SET()`を使用する。
この時変数に格納する値は文字列かつカンマ区切りかつスペース無しでなければならない。

```
SET @keys := '1,2,3,4,5';
SELECT *
FROM table
WHERE FIND_IN_SET(key, @keys)
;
```

## 文字数カウント

`CHAR_LENGTH()`を使う。
バイト数ではなく文字数を取得してくれる。
マルチバイトでも文字数を取得してくれる。

```
SELECT CHAR_LENGTH(column)
FROM table
;
```

## カラム属性の変更

```
ALTER TABLE table
CHANGE old_column new_column type COMMENT ''
;
```

## JSON型カラムを問い合わせ条件にする

```
SELECT *
FROM table
WHERE JSON_EXTRACT(value, '$.key')
;
```

[MySQL :: MySQL 8.0 リファレンスマニュアル :: 11.5 JSON データ型](https://dev.mysql.com/doc/refman/8.0/ja/json.html)

