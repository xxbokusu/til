# TIL(Today I Learned)

This repository is to write my result of daily learning

# 4/1 jenkinsとslack連携の話
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
