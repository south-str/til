# Docker

Dockerのドキュメントは以下にある。

[Docker Docs](https://docs.docker.com/)

有志による翻訳は以下にある。

[Docker ドキュメント日本語化プロジェクト — Docker-docs-ja 27.0 ドキュメント](https://docs.docker.jp/)

## バージョン出力

`docker --version`を使う。

```
$ docker --version
Docker version 29.2.0, build 0b9d198
```

## ローカルに存在するイメージの一覧

`docker images`を使う。

```
$ docker images
                                                                                                                                        i Info →   U  In Use
IMAGE           ID             DISK USAGE   CONTENT SIZE   EXTRA
amazonlinux:1   115d9edf5dba        169MB             0B        
```

## ローカルに存在するコンテナの一覧

`docker ps`を使う。

## イメージを使ってコンテナを起動する

`docker run`を使う。

## コンテナを停止する

`docker stop [container id]`を使う。

## コンテナを削除する

`docker rm [container id]`を使う。

### Apple Siliconでamd64向けのイメージを実行する

Docker DesktopのSettings→Generalから`Use Rosetta for x86/amd64 emulation on Apple Silicon`にチェックをいれる。
さらに`docker run --platform linux/amd64 [image name]`のようにオプションをつけて実行する。
ただこのままでは起動したイメージにログインできないので
`docker run --platform linux/amd64 --interactive --tty --rm [image name]`
を実行する。

## Docker Hubのイメージを使用してAmazon Linux1をローカルで実行する

1. イメージをpullする
    - `docker pull --platform linux/amd64 amazonlinux:1`
2. コンテナを起動する
    - `docker run --platform linux/amd64 --interactive --tty --rm amazonlinux:1`

これで起動したコンテナにログインした状態となる。

オプションについては`docker help run`で一覧を見ることができる。

- `-i, --interactive`:Keep STDIN open even if not attached
- `-t, --tty`:Allocate a pseudo-TTY
- `--rm`:Automatically remove the container and its associated anonymous volumes when it exits

ボリューム(コンテナ内のデータ)を残したい場合は`--rm`オプションを付けてはいけない。

## no matching manifest for linux/arm64/v8 in the manifest list entriesエラーが発生してイメージをpullできない場合の対処について

イメージを取得しようとしても失敗する。

```
$ docker pull amazonlinux:1
1: Pulling from library/amazonlinux
no matching manifest for linux/arm64/v8 in the manifest list entries
```

CPUが対応していないのでダメっぽいが、調べたら`--platform linux/amd64`を指定したりダイジェストを指定したりするといけるかもしれない。

```
$ docker pull amazonlinux@sha256:6836a8934245ec840a17e1a16f2f060a04fbc8a2a4ace322d46218c0933a1374
docker.io/library/amazonlinux@sha256:6836a8934245ec840a17e1a16f2f060a04fbc8a2a4ace322d46218c0933a1374: Pulling from library/amazonlinux
no matching manifest for linux/arm64/v8 in the manifest list entries
```

ダイジェスト指定はダメだった。
`--platform`を使ってpullで持ってくるイメージのアーキテクチャを固定する。

```
$ docker pull --platform linux/amd64 amazonlinux:1
1: Pulling from library/amazonlinux
dec7ae9c3829: Pull complete 
Digest: sha256:6836a8934245ec840a17e1a16f2f060a04fbc8a2a4ace322d46218c0933a1374
Status: Downloaded newer image for amazonlinux:1
docker.io/library/amazonlinux:1

What's next:
    View a summary of image vulnerabilities and recommendations → docker scout quickview amazonlinux:1
```

無事にpullされた。

