# git

## リモートにpushした後にcommitterとauthorが間違っていることに気付いた時

過去のコミット情報にあるCommitterとAuthorを変更する。

```sh
git filter-branch -f --env-filter "GIT_AUTHOR_NAME='[author-name]'; GIT_AUTHOR_EMAIL='[author_email]'; GIT_COMMITTER_NAME='[committer-name]'; GIT_COMMITTER_EMAIL='[committer-email]';" HEAD
```

最後の`HEAD`で変更するコミット範囲を指定しているため、直近n個目(`@~n..@`だと思うが自信がない)までという指定もできる。

実際に変更されたかどうかは`git log --pretty=full`で確認できる。

既にpushしてしまった後である場合はリモートに変更したことをpushしなければならない。
この時は`-f`オプションが必要となる。

```
git push -f origin [branch-name]
```

## stashに名前をつけたい

`git stash save`を行うと直前のコミットメッセージが表示され、後々`git stash list`で一覧を表示した時に作業内容を把握することができない。

`git stash save [<message>]`の形式で実行するとメッセージを登録することができるため、現在の作業内容を端的に示すことができる。

```
git stash save "issue0000対応(wip)"
```

という感じになる。詳細は`man git-stash`を参照。

## pre-commitで`php -l`をする

commit前にlintを動かしたいと思ったので、その設定方法を調べた。`php -l`と`php --syntax-check`は同じ。

git管理ディレクトリである.gitの中にあるhooksディレクトリにサンプルがあるので、それを参考にして以下のようなファイルを作成した。

```sh
#!/bin/sh

# 基準となるcommitを取得している? .git/hooks/pre-commit.sampleから拝借した
if git rev-parse --verify HEAD >/dev/null 2>&1
then
  against=HEAD
else
  # Initial commit: diff against an empty tree object
  against=$(git hash-object -t tree /dev/null)
fi

# 変更/追加したファイルの一覧を取得する
files=$(git diff --cached --name-only --diff-filter=AM)
echo $files
# 取得したファイル一覧をリストとしてphpのlintを実行する
for file in $files; do
  php --syntax-check $file
  if [ $? != 0 ]; then
    echo 'abort commit'
    exit 1
  fi
done

echo 'syntax ok'
exit 0
```

これを`.git/hooks/pre-commit`として保存すれば、commit前にこのスクリプトが実行される。

注意として、このスクリプト自体をgitで管理することはできない。そのため、他の開発者にも使用してもらいたい場合は別のディレクトリで管理しておいてそちらを参照する設定にするか、開発環境をセットアップする際にhooksへコピーするようなスクリプトを別途用意しておかなければならない。

それとエラーが起きたファイルを修正したら`git add`を忘れないように。stagingされていないので、他のファイルだけcommitされてしまう。
