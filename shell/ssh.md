# ssh

## バージョン違いで発生したこと

OpenSSL6から9の環境に移行したときに、過去の設定のままではssh接続を行えなかった。
(エラーが発生した)

認証鍵のアルゴリズムが古いものであったため、sshクライアントが拒否したのが原因だった。
`.ssh/config`に以下の設定を追加したことでエラーなく実行されるようになった。

```
HostKeyAlgorithms +ssh-rsa
PubkeyAcceptedKeyTypes +ssh-rsa
```

また、ssh-agentに登録している鍵が多いと特定の鍵を使わずに認証を行うことがあった。
以下の設定を追加したことで特定の鍵で認証を行うようになった。

```
IdentitiesOnly yes
```

