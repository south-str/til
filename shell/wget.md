# wget

## Amazon Linuxでwgetをビルドする

- ソースコードをダウンロードする
- configureファイルを実行する
- make installする

### ソースコードをダウンロードする

```
wget https://ftp.gnu.org/gnu/wget/wget-latest.tar.gz
```

### configureファイルを実行する

ダウンロードしたファイルを`tar -zxvf wget-latest.tar.gz`で展開する。

その後展開されたディレクトリに移動して`./configure`を実行するが、その前に足りないライブラリをインストールする。

```
sudo yum install gcc72 openssl-devel -y
```

その後オプションをつけて`./configure`を実行する。

```
./configure --with-ssl=openssl --prefix=[インストール先ディレクトリ]
```

Summary of build optionsが表示されたらmake可能と思われる。

### make installする

```
make install
```

prefixに指定したディレクトリにbinやshareディレクトリが作成されている。binディレクトリの中にwgetが作成されているので、`ldd ./wget`でlibsslがリンクされているか確認する。

作成したwgetはもちろんパスが通っていないため、実行する際は明示的にパスを指定する必要がある。

