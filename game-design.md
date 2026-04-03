# ミニマルブラウザゲームの設計・構成案

A Dark Room（https://github.com/doublespeakgames/adarkroom）のようなミニマルなテキストベースのゲームをitch.ioで公開するための設計・構成メモ。

---

## コンセプト

- **ジャンル**: テキストベースのインクリメンタル/アドベンチャーゲーム
- **スタイル**: ミニマルUI、テキスト中心、クリックで進行
- **公開先**: itch.io（HTML5ゲームとして埋め込み公開）
- **要件**: インストール不要、ブラウザだけで誰でも遊べる

---

## 技術スタック

| 役割 | 選択肢 | 理由 |
|------|--------|------|
| 言語 | Vanilla JS（TypeScript推奨） | 外部依存なし、軽量 |
| ビルド | Vite | 設定が最小、itch.io用zipを簡単に出力 |
| スタイル | CSS（変数使用） | フレームワーク不要、ミニマルUI向き |
| 状態管理 | 自前のシンプルなStore | Reduxは過剰、ゲーム状態はPOJOで十分 |
| 保存 | localStorage | サーバー不要、オフライン対応 |

> Reactなどのフレームワークは使わない。ゲームループとDOM操作を直接制御した方がシンプル。

---

## ディレクトリ構成

```
my-game/
├── index.html          # エントリーポイント（itch.ioが読み込む）
├── src/
│   ├── main.ts         # 初期化・ゲームループ起動
│   ├── state.ts        # ゲーム状態（POJO + イベントバス）
│   ├── engine/
│   │   ├── tick.ts     # 時間経過ロジック（setInterval）
│   │   └── events.ts   # イベントシステム（観察者パターン）
│   ├── scenes/
│   │   ├── room.ts     # 最初の部屋シーン
│   │   ├── world.ts    # 外の世界シーン
│   │   └── ...         # シーンを追加していく
│   ├── ui/
│   │   ├── render.ts   # DOM更新（差分更新、仮想DOMなし）
│   │   ├── log.ts      # メッセージログ表示
│   │   └── buttons.ts  # ボタン生成・管理
│   └── data/
│       └── strings.ts  # テキスト・ナラティブデータ
├── style.css
├── vite.config.ts
└── package.json
```

---

## アーキテクチャの核心

### 状態管理

```typescript
// state.ts
export const State = {
  game: {
    heat: 0,
    wood: 0,
    tick: 0,
  },
  get(key: string) { ... },
  set(key: string, value: any) {
    // 状態更新 → イベント発火 → UI再描画
  }
}
```

### ゲームループ（tick駆動）

```
setInterval → tick() → 状態更新 → イベント発火 → render()
```

- A Dark Roomと同様、時間経過で状態が変化するインクリメンタル設計
- tick間隔は調整可能（デフォルト1秒）

### シーン分割

- 各シーンは独立したモジュール
- `scene.enter()` / `scene.tick()` / `scene.render()` のインターフェースで統一
- シーンマネージャーがアクティブシーンを管理

### UIの更新

- 仮想DOMは使わず、`render()` で必要なDOM要素だけ更新
- メッセージログは配列で管理し、新規メッセージだけ追記

---

## itch.io公開フロー

1. `vite build` で `dist/` に出力
2. `dist/` フォルダをzip圧縮
3. itch.ioに新プロジェクト作成
   - Kind of project: **HTML**
   - `index.html` が起動するようにzip構成を確認
4. Embed options で **Click to launch in fullscreen** を設定
5. 公開 → URLをシェア

> itch.ioはHTML5ゲームをiframeで実行するため、外部通信が不要なゲームなら完全動作する。

---

## 開発ステップ（推奨順）

1. [ ] Viteプロジェクトセットアップ（`npm create vite@latest`）
2. [ ] 最小ゲームループ実装（tick + ログ表示だけ）
3. [ ] 最初のシーン（暗い部屋 → 火をつける）
4. [ ] リソース管理（wood, food など）
5. [ ] セーブ/ロード（localStorage）
6. [ ] 追加シーン・ナラティブ
7. [ ] itch.ioにデプロイ・テスト

---

## 参考

- [A Dark Room ソースコード](https://github.com/doublespeakgames/adarkroom)
- [itch.io HTML5ゲームの作り方](https://itch.io/docs/creators/html5)
- [Vite](https://vitejs.dev/)
