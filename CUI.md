## "|"についてのわかり
コマンドでパイプ`|`を使う時の`echo`ってプログラムに対して`echo`の文章を渡すって意味だったのね。
```
echo list disk | diskpart
```
参考：https://win.just4fun.biz/?%E3%82%B3%E3%83%9E%E3%83%B3%E3%83%89%E3%83%97%E3%83%AD%E3%83%B3%E3%83%97%E3%83%88/%E3%83%87%E3%82%A3%E3%82%B9%E3%82%AF%E4%B8%80%E8%A6%A7%E3%82%84%E3%83%91%E3%83%BC%E3%83%86%E3%82%A4%E3%82%B7%E3%83%A7%E3%83%B3%E6%83%85%E5%A0%B1%E3%82%92%E7%A2%BA%E8%AA%8D%E3%81%99%E3%82%8B%E3%83%BBdiskpart

## ↑のechoにパイプかましてもPermissionが邪魔で上手くいかない～
Windowsの設定を弄ろうとしても（https://blogger.zatsuroku.net/2017/11/blog-post_12.html）互換性の設定がないんだよね…
仕方ないので、Cygwinからsudoで叩こうとしてみる
