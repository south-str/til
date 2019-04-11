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
