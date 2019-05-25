## "|"についてのわかり
コマンドでパイプ`|`を使う時の`echo`ってプログラムに対して`echo`の文章を渡すって意味だったのね。
```
echo list disk | diskpart
```
参考：https://win.just4fun.biz/?%E3%82%B3%E3%83%9E%E3%83%B3%E3%83%89%E3%83%97%E3%83%AD%E3%83%B3%E3%83%97%E3%83%88/%E3%83%87%E3%82%A3%E3%82%B9%E3%82%AF%E4%B8%80%E8%A6%A7%E3%82%84%E3%83%91%E3%83%BC%E3%83%86%E3%82%A4%E3%82%B7%E3%83%A7%E3%83%B3%E6%83%85%E5%A0%B1%E3%82%92%E7%A2%BA%E8%AA%8D%E3%81%99%E3%82%8B%E3%83%BBdiskpart

## ↑のechoにパイプかましてもPermissionが邪魔で上手くいかない～
Windowsの設定を弄ろうとしても（https://blogger.zatsuroku.net/2017/11/blog-post_12.html）互換性の設定がないんだよね…
仕方ないので、Cygwinからsudoで叩こうとしてみる

## sedで任意のファイルの任意の行にdumpを仕込めるようにすると色々捗りそう
> insert-dump [file] [line_number]

こいつをエイリアスとして↓でよいはず
> sed -i -e '1[line_number] hoge' [file]

参考 :  https://www.atmarkit.co.jp/ait/articles/1610/13/news015.html
        https://www.na3.jp/entry/20110310/p1
        
Macだとこれでできない。えっ
> sed: 1: "/2/a hoge": command a expects \ followed by text

検索をかけても `gnu-sedを使えばよい` など「そういうこと訊いてるんじゃないのだが…」って解法が目立つ（それを素直に受け取れたほうが良いのかもしれないが」
で、最終的な参考： https://detail.chiebukuro.yahoo.co.jp/qa/question_detail/q10171612785
> sed -i -e '[line_number]i\'$'\n'' hoge' [file]

これでいい。結論、 `sed` コマンドはめんどい！
