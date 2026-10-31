# 絵・図・スライドの描画は cloudflare-tools を使う

絵やスライドの図が必要なときは、GitHub の非公開リポジトリ `tiezox/cloudflare-tools` を使う。手順の本体はそのリポジトリの `CLAUDE.md` にあるので、使う前に読む。セッションにそのリポジトリを追加するか、次のコマンドで取得する。

```bash
gh api repos/tiezox/cloudflare-tools/contents/CLAUDE.md --jq .content | base64 -d
```

仕組みの要点は次の4つである。

- 絵は Cloudflare Workers AI(FLUX.1 schnell)で生成する。そのリポジトリの GitHub Actions `generate-image.yml` を実行すると、`images/<名前>.jpg` と指示文 `images/<名前>.txt` が main にコミットされる。
- 絵の中に文字を描かせない(崩れる)。見出し・箱・矢印・説明文は Claude が HTML/SVG で組み、挿絵だけ生成画像を埋め込む。PNG にするときはクラウド環境の Chromium でスクリーンショットを撮る。
- 無料枠は1日1万 Neuron(1024×1024・4ステップで約170枚)で、日本時間 9:00 にリセットされる。
- 認証情報はそのリポジトリの GitHub Actions シークレットにだけ置く。Claude は値を読まない・表示しない・ログに出さない。ユーザーにチャットへ貼らせない。

なぜ: 描画の道具と認証情報を1か所にまとめ、どのリポジトリからも同じ手順で使えるようにするためである。
