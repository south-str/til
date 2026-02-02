# diff

## gitと同じ形式で差分を取る

`-u`オプションを使用する。

```
diff -u first.txt second.txt
```

## 差分に色をつける

`--color`オプションを使用する。

```
diff --color first.txt second.txt
```

`--color=[when]`のwhenには`never, auto, always`が適用できる。

`always`だとパイプで渡した後も色をつけてくれる。

