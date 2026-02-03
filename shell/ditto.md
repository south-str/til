# ditto

macOSのコピーツール兼アーカイバである。
zipコマンドだとWindowsで開いた時に正常に開けない問題があるが、`ditto`であればそれがない。

## 基本的な使い方

```
ditto sourceDirectory archive
# -cオプションでアーカイブを指定したパスに作成し、-kオプションでzipにする
ditto -ck exampleDirectory exampleDirectory.zip
# --sequesterRsrcオプションを追加するとmacOSのメタデータを隔離し、Windowsから見えなくする
ditto -ck --sequesterRsrc exampleDirectory exampleDirectory.zip
```

複数アーカイブしたい場合はファイルではなくディレクトリを指定する。

