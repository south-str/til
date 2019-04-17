# less

`less`コマンドについて

## Macでは`less`コマンドでgzipされたファイルを閲覧できないのはなぜか

Linux環境では`less`でgzipされたファイルを閲覧できるが、Macではできない。

Linux環境では環境変数`LESSOPEN`に`lesspipe.sh`というシェルスクリプトが定義されているため。

```sh
$ env | grep LESS
# LESS_TERMCAP_mb=
# LESS_TERMCAP_md=
# LESS_TERMCAP_me=
# LESS_TERMCAP_ue=
# LESS_TERMCAP_us=
# LESSOPEN=||/usr/bin/lesspipe.sh %s
# LESS_TERMCAP_se=
```

Macでは環境変数`LESSOPEN`に何も定義されていない。

```sh
$ env | grep LESS
# LESS_TERMCAP_mb=
# LESS_TERMCAP_md=
# LESS_TERMCAP_me=
# LESS_TERMCAP_ue=
# LESS_TERMCAP_us=
# LESS_TERMCAP_so=
# LESS_TERMCAP_se=
```

`lesspipe.sh`でgzip形式の拡張子である場合以下のように処理をしている。

```sh
*.[zZ]|*.gz) gzip -dc -- "$1"; handle_exit_status $? ;;
```

つまり`gzip -dc | less`のようなことを行なっているようだ。
BSDのgzipも`-d(--decompress, --uncompress)`と`-c(--stdout, --to-stdout)`のオプションは同じなので、同様のコマンドを打てばMacでもgzipファイルを`less`で閲覧することができる。

