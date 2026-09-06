# 新居コスト電卓

新居の家賃・管理費・駐車場・光熱費を入力すると、今の家との差額を入力のたびにリアルタイムで計算する、スマホ向けの1ファイル電卓アプリです。

外部依存・バックエンドなし。`index.html` 1枚で完結します（Google Fonts の読み込みのみ外部通信あり）。

画面右上の ⚙ から設定画面を開くと、「今の家」の内訳（家賃実費・管理費・駐車場・ネット・電気・ガス）と住宅手当のルール（率・上限額）をいつでも変更できます。設定はブラウザの localStorage に保存されるため、同じ端末・同じブラウザで開けば次回も引き継がれます（別の端末やブラウザには同期されません）。

## ローカルで試す

`index.html` をブラウザで直接開くだけで動作します。

```bash
# このフォルダで簡易サーバーを立てても可（任意）
python3 -m http.server 8000
```

## GitHub Pages で公開する

1. このフォルダの中身（`index.html` など）をGitHubの新しいリポジトリにpushする

   ```bash
   git init
   git add .
   git commit -m "Add new home cost calculator"
   git branch -M main
   git remote add origin https://github.com/<ユーザー名>/<リポジトリ名>.git
   git push -u origin main
   ```

2. GitHubのリポジトリページで **Settings → Pages** を開く
3. **Source** を `Deploy from a branch` にし、Branch を `main` / `/(root)` に設定して **Save**
4. 数分後、`https://<ユーザー名>.github.io/<リポジトリ名>/` でアクセスできるようになります

## 現在の家の基準値を変更したい場合

`index.html` 内、`<script>` タグの中にある以下の定数を書き換えてください。

```js
var CURRENT_MONTHLY_COST = 52200; // 現在の家の実質月額
var MAX_ALLOWANCE = 50000;        // 住宅手当の上限
```

住宅手当の計算式（家賃 × 50%、上限あり）を変えたい場合も同じ関数 `recalc()` 内で調整できます。
