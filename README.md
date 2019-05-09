# TIL(Today I Learned)

This repository is to write my result of daily learning

## 4/1 jenkinsとslack連携の話
Jenkins⇒Slackで通知を飛ばす方法を学んだ。
> 参考：https://qiita.com/ryuthky_github/items/c7e68fba13ddf230159a

JenkinsとSlackのそれぞれの設定ページで連携を設定すると1 vs 1の紐づけができる。
ただし、この設定だとjenkinsジョブから1つのチャンネルにしか通知を飛ばせない。

## ここで、1つのjenkisジョブから複数のSlackチャンネルに対して通知を出し分けたい場合を考える。
> 参考：https://qiita.com/ik-fib/items/b4a502d173a22b3947a0

Slack側の連携ツール「Incoming webhooks」を使用する。
通知を受け取るためのアプリケーションであり、Add Configurationすることで、Slack通知の送付先（End point）をURLの形で得られる。
このIncoming webhooksの設定を送信したいチャンネルの数だけ生成して、それぞれに対してcurlでメッセージを送ることで実装したい機能を実現する。
> curl -X POST --data-urlencode "payload={\"text\": \"TEST\" }" https://~~

## 4/2 fab（fabric）の仕様について調べる
参考：ドキュメントのチュートリアル部分　https://fabric-ja.readthedocs.io/ja/latest/tutorial.html
- 直訳だから中々にイカした文章

pythonの機能をシェルスクリプト的に実行するためのツール(remote execution tool)である。
pythonで記載した関数（ex. deploy）を`fab deploy`などとコマンドライン城で実行するだけで機能させることができる。
scriptであり、ここからさらにローカルでのコマンド実行やリモートでの操作を誘発できるのでできることはかなりい多い。

上記のチュートリアルでも、一つのコマンド実行でテスト→gitへのpush→deployまでを実現している。。

タスクへの引数も渡しやすく作られている。
他、参考：https://qiita.com/momota10/items/030d12449f36d788a5b7

## 4/2 rebase運用とは
rebase運用が履歴の改変をするため危険ということは理解している。
ここでは`git pull --rebase`の話
> https://www.lancard.com/blog/2016/11/07/git-rebase-and-pull-rebase/

見る限り基本的には問題なさそう？？？
> http://kray.jp/blog/git-pull-rebase/

とはいえ立派な宗派争いみたいだ。
rebaseは基本的に履歴を改変して見栄え的に綺麗な形につくり変えるものと理解して良さそう。
個人的な感覚としてはあまりやりたくはないかな

## 4/3 リンクメモ：「物乞い」→路上ディベートへの派生が面白い話。
> https://medium.com/@kihapper/欧州の都市における-ものごい-をデザインする-557581521f3b

物乞いが尊厳を取り戻せる仕事とは？という試行実験の中でストリートディベートというより大きな問題にアプローチできる手法を発案したという話。
もちろん、同じことが日本でできるかというと、議論をする土壌がないため難しいかな、というところ。

でもこれこそが複数の問題を一挙に解決する”アイデア”という概念そのものだよね、というわかりを得た。

こういう発明はどのように生まれるのか？
このケースだと日常で見つけた身内の困難を解決したい一心で試みた施策の一つについて別の解釈をするとこういう手法になるよね？って解釈できたケース。
もしかしたら別の人の目を通した時に「これってこうじゃね？」と解釈が生まれたのかもしれないし、試行の中で通りがかった人の反応を見て気づいたのかもしれない。

### つまるところ思いつきはどんどん形にしてアウトプット→人の目を介することで初めて意味を、解決する問題を得て「アイデア」になるのでは？？？という結論

## 4/8 キャッシュの扱いに困る問題
参考：http://aimstogeek.hatenablog.com/entry/2018/01/17/154537
とはいえキャッシュの話がまだまだわからない。
使い分けとしてはここが参考になりそう：https://academy.gmocloud.com/know/20160125/1584
- ローカルキャッシュ：サーバ側に誰もが使うデータをキャッシュする。分散環境には向かない
- 分散キャッシュ：MemCachedが含まれる。分散化されて利用することを想定している。Web経由で使う？？？
- クライアントサイドキャッシュ：クライアント側でユーザよりの内容を保持する仕組み
- DBキャッシュ：DBから読み出す内容のキャッシュ。クエリと結果を紐づけて保持するということはローカルキャッシュに近い？？？

## 4/9 端末（Session?)作成コマンドtmuxの導入
> brew install tmux

これだけで使える！
> Ctrl+b -> % で分割
> Ctrl+b -> d で切断
> tmux a でセッション復帰

## GASってなんだ？
Google Apps Script
参考：https://qiita.com/t_imagawa/items/47fc130a419b9be0b447
Chromeの拡張機能として導入できてDrive上のコンテンツと連携できるみたい。
なお連携できるのはContainer Bound Scriptのみの模様

Googleが公開しているライブラリもあるみたい！：https://github.com/gsuitedevs/apps-script-samples

## 4/15 システムのパフォーマンスってなんぞやって話
ひとまず参考：https://www.oracle.com/technetwork/jp/ats-tech/tech/useful-class-7-520780-ja.html
大型Webシステムの運用時のパフォーマンス測定基準が書いてあるので参考にできる気がする。
> 1. 同時接続ユーザー数(Number of Virtual Users)
> 2. 時間あたりのユーザーシナリオ実行本数(Transactions per hour)
> 3. 時間あたりのページ処理数(Received pages per hour)
> 4. 時間あたりのヒット数（Hits per hour）
> 5. サーバー平均応答時間(Average Server times, etc.)
> 6. サーバー側のCPU使用率

1.はいわゆるDAU（Daily Active User）だから、ユーザーにIDがあれば基本的なアクセスログから抜き取れる。ソシャゲなら一種のKPIとして使われてるはず。
でも、ログインボーナスだけのユーザもいるから直接1.をシステムのパフォーマンス良し悪しの判断基準にすることは危険よなぁ

2〜4はサーバの処理性能として役立ちそう。
2, 3の差分が若干わからなかったけどページに含まれるコンテンツ量でもって判断するとよいようで納得。
コンテンツの大小にページ間で差があって、読み込みでかかる負荷が変わる場合はヒット数を使うそう。

逆にヒット数という指標はユニークなユーザ数が得られない環境においては、平均ヒット数でもってユーザ数の推定に使えるそうな
あとはDBアクセス数も別の負荷基準として使えるか。
5.はクライアント側が存在する環境だと、ユーザ側に依存する部分が大きいからサーバ側を最速にする以外の対応はできないなぁ。

とはいえ、テスト環境と本番環境だと性能差があるから信頼できる測定値ってむずいなぁ

コマンドでの測定はこっちhttps://qiita.com/toshihirock/items/0e0b20064730469e93e6

### 4/17 追記　Perl専用だけどツールを習ったNYTProfというプロファイラ
https://tutorial.perlzemi.com/blog/20100507127089.html
ひとまずプロファイラというツールの使い方や使用感はやってみて覚えるとする。

あとアウトプットについて、ちょっと気になる記事に行き当たったので
https://note.mu/fromdusktildawn/n/nb7ee5a557447

アウトプットの出し方の部分でちょっと思い当たる節がありすぎるので変えていきたい。
実践を通してこそを理解として初めてアウトプットを生成する、ってすればどうにかモノになるか…？

## 5/7 A tour of Goにとりかかった
https://go-tour-jp.appspot.com/welcome/1

5/8 時点でMethods and interfacesの手前まで進行中。

## 5/9 ゲーム関連の論文サーベイってやってみたい
- Python
ここかなぁ : Aidemy： https://aidemy.net
もうちょっと短時間のやつ：https://www.programiz.com/python-programming/tutorial
    多分DataCampってサイトに登録が必要

## 5/9 Go言語以外の言語についてもツアーってないのかな
ResearchMap作成に取り組んだ？ってやつ
- https://researchmap.jp/mu8xrm15g-1918131/?action=multidatabase_action_main_filedownload&download_flag=1&upload_id=133467&metadata_id=107646
    - 「多岐にわたりすぎる」ってちょっと諦め気味なので、分類分けして絞らないと自分でやるのも難しそう
