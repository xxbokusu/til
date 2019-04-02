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
