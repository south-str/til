# su

`su`コマンドについて

## ユーザ変更をした時に特定のPATHを環境変数に追加したい

`/usr/local/bin`を常に`$PATH`に設定しておきたい時は、変更先ユーザのホームディレクトリにある`.bashrc`を編集する。
`.bash_profile`では`su`でユーザ変更した時に反映されないので意味がない。

例えば以下のように`.bashrc`へ追加する。

```sh
PATH=$PATH:/usr/local/bin
```

