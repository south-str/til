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
