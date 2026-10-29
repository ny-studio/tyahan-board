# チャーハンワールド 全国番付（公開用）

VRChat のワールド「チャーハンを作る」（武威或飯店）の、全国番付と、作ったチャーハンの量のワールド累計を置く所。
ワールドは `https://<ユーザー名>.github.io/<リポジトリ名>/board.txt` を読む。

- Actions が 10 分おきに、中継（Cloudflare Workers）の `/board` を取り、`board.txt` を更新する（Actions タブで一度 `board` を手動実行すると確認できる）
- `board.txt`: 1 行目 `#updated<TAB>時刻`、その後ろに点の順位（`順位<TAB>名前<TAB>点 × 10`）、`#grams<TAB>ワールドの合計 g<TAB>人数` と、作った量の順位（`順位<TAB>名前<TAB>g`）
- Settings → Pages は「Deploy from a branch / main / (root)」

## 秘密にするもの

このリポジトリは公開なので、中継の URL もファイルに書かない。
Settings → Secrets and variables → Actions → **Secrets** に `BOARD_URL`（= `https://<中継>/board`）を入れる（Variables ではなく Secrets。ログに出ても伏せられる）。
PlayFab のタイトル ID と秘密の鍵は、中継の側にだけある（ここには要らない）。
入れてからでないと `board` のワークフローは落ちる（board.txt は古いまま残るので、ワールドの表示は壊れない）。
