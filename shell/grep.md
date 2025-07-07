# grep

## 特定のディレクトリを除いて検索する

`--exclude-dir`オプションを使用する。

```
grep -r --exclude-dir='log' [pattern] [file]...
```

## 特定の拡張子のファイルのみ検索する

`--include`オプションを使用する。

```
grep -rn --include='*.md' [pattern] [file]...
```

