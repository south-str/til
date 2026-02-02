# JavaScript

## Bookmarklet

Mac Safariで動作確認済み。

### Markdownのリンク形式でサイトのタイトルとURLをコピーする

```
javascript:(function(d)%7Bprompt(%22Copy%20Title%20and%20URL%20for%20Markdown.%22,'%5B'+d.title+'%5D('+d.location.href+')');%7D)(document);
```

### サイトに表示されている広告を非表示にする

一部のタグを消しているだけなので広告かどうかを判別しているわけではない。

```
javascript:['ins','iframe','[class*=ads]','[class*=third-party]','[class*=gliaplayer]','[class*=trv-player]','[id*=third-party]'].forEach(a=>document.querySelectorAll(a).forEach(b=>b.remove()));
```

