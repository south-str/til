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

