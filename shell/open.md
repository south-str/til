# open

OS X用のツールであるopenについて

## パイプでアプリケーションにデータを渡したい

例えばあるファイルの先頭10行をNumbersで見たい場合は以下のようにする。

```sh
head -n 10 something.csv | open -f -a Numbers
```

`-f`オプションで標準出力のデータを入力にすることができる。
`-a`オプションで特定のアプリケーションを起動することができる。

`-a`オプションを使用しない場合はデフォルトのテキストエディタ(テキストエディット)が起動される。
