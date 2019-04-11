## 開発の覚書
- Readmeに開発環境を書いておかないと後で使う人の時間を浪費させてしまうな、と
  - Unityのバージョン、ビルド設定

## アプリをBuildした時のデバッグってどこでやるんだろ？
常に実機上？違う気がする
PC上で.apkをクリックするとNox Playerで起動してくれたのでこれはこれで結構よいかも

## 4/8 配置したTextが表示されないんだが～
Canvas上に配置したオブジェクトに収まらないサイズのフォントを置くと非表示になる模様。
Powerpointなどとは違う感じだったから気づかんかった…
ObjectのWidthとHeightを大きくするように弄って解決

## 4/11 UnityをGitRepositoryに追加するときの戦い
https://qiita.com/sodaihirai/items/caf8d39d314fa53db4db
↑の手順に従って
> git add -A

をした時が今回のエラー。
```
error: open("Temp/UnityLockfile"): Permission denied
error: unable to index file Temp/UnityLockfile
fatal: adding files failed
```
参考：https://qiita.com/A-Kouki/items/d63c77bc5527a4f4cb7f
問題のtmpファイルはUnityを開いてる時だけ存在する奴。Unityを閉じたら出なくなって万々歳

機嫌よくremoteにpushしようとしたら次はコレ
```
$ git push origin master
To https://~~
 ! [rejected]        master -> master (non-fast-forward)
error: failed to push some refs to 'https://~~'
hint: Updates were rejected because the tip of your current branch is behind
hint: its remote counterpart. Integrate the remote changes (e.g.
hint: 'git pull ...') before pushing again.
hint: See the 'Note about fast-forwards' in 'git push --help' for details.
```
> git pull --rebase origin master

でremoteに一致させて解決
次はgitignoreをセットしてMacで開くテストだ！
