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
> git init

して
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
> git remote add origin [remote repositry]

次はgitignoreをセットしてMacで開くテストだ！

## 4/15 gitignoreを反映していざ、って件
いよいよ.gitignoreを作ってRepositoryに反映。
WindowsとMacで共同開発を狙ってみた。

gitignoreは　https://www.cg-method.com/entry/unity-gitignore-setting/ を参考に作成。
http://astlab.jp/開発ツール/git/gitignoreを後から追加 にしたがって、
> git rm -r --cached .

を実行して反映した。
いざ、pullしてOpen！　UnityHubでバージョン合わせをサボったので、
> 	modified:   ProjectSettings/ProjectVersion.txt

と出てしまう。気をとりなおしてUnityHubにWindowsと同じバージョンをロード。
やり直すと消えたけど今度は
> Assets/Editor/com.unity.mobile.notifications/NotificationSettings.asset

確認して対応しなきゃなー。見た感じ必要なパッケージが入ってないだけだけど一旦寝かせておく方向で。

## 6/13 ゲーム開発をする際にはつかえそうなやつ
おすすめのOSSツール
http://baba-s.hatenablog.com/entry/2018/03/23/090000

Unity List
https://unitylist.com/browse?f=projects

3月のゲームジャムの作品
https://unityroom.com/games/animal_circle

ここから素材元を参考にする
BGM/フリー素材
- https://soundeffect-lab.info/
- https://maoudamashii.jokersounds.com/
- https://pocket-se.info/
- https://dova-s.jp/_contents/author/profile000.html
- https://assetstore.unity.com/packages/audio/sound-fx/pro-sound-collection-50235
- https://soundcloud.com/sebaschan201/sets/hexera-romance
- https://www.hurtrecord.com/bgm/56/
- https://dova-s.jp/bgm/play1889.html
- https://soundrium.com/
- http://pansound.com/panicpumpkin/

アニメーション全般
https://assetstore.unity.com/packages/tools/animation/dotween-hotween-v2-27676

フォント素材
http://www17.plala.or.jp/xxxxxxx/00ff/

by https://unityroom.com/games/block_connect

サンプルUI素材
https://assetstore.unity.com/packages/essentials/unity-samples-ui-25468
UI Effect
https://github.com/mob-sakai/UIEffect
SimpleUI
https://assetstore.unity.com/packages/2d/gui/icons/simple-ui-103969

日本語入力
https://github.com/unity3d-jp/WebGLNativeInputField

リアルタイムマルチプレイヤーライブラリ
https://assetstore.unity.com/packages/tools/network/photon-unity-networking-classic-free-1786

ネットワーク周り
https://assetstore.unity.com/packages/tools/network/pun-2-free-119922

定番ライブラリ？
UniRx 使い方（https://www.slideshare.net/torisoup/unity-unirx )
https://assetstore.unity.com/packages/tools/integration/unirx-reactive-extensions-for-unity-17276

Effect
https://assetstore.unity.com/packages/tools/particles-effects/flatfx-2d-effects-102072

## 6/27 WebGLビルドを試してみた
https://blog.naichilab.com/entry/2017/04/29/125527
ここでの手順通りにして2Dゲームについても`Build And Run`できることを確認
https://assetstore.unity.com/packages/essentials/tutorial-projects/2d-ufo-tutorial-52143

オープンソースな2DゲームをいくつかDLすれば、それらの組み合わせでゲームを作れるか…？

## 7/2 画面の一部を黒で塗りつぶす
SpriteとShaderを使って実現する
http://games.genieus.co.jp/unity/unity2d_mask/

マスクを半透明に : http://tsubakit1.hateblo.jp/entry/2017/11/24/020430#%E5%8D%8A%E9%80%8F%E6%98%8E%E3%81%8C%E5%95%8F%E9%A1%8C

背景までくり抜かれて描画順を工夫しても上手くいかない…どういうことだ…
http://ghoul-life.hatenablog.com/entry/2017/06/26/202035

## 7/3 音を出したい！！
お手本の中を探した : ↑の中の　PsychoMothers/Assets/PsycthoMothers/Scripts/Battle/Manager/AudioManager.cs
Audio Managerクラス : http://kan-kikuchi.hatenablog.com/entry/AudioManager
その２　http://kan-kikuchi.hatenablog.com/entry/AudioManager2

