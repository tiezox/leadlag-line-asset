# SEC のページは、連絡先を名乗って開く

SEC(米国証券取引委員会)のサイトのページをプログラム(`curl` など)で取りに行くときは、道具の名前と連絡先を名乗る。`www.sec.gov` は、名乗りが無いと 403 で断る(ページの題名が「Your Request Originates from an Undeclared Automated Tool」になる)。名乗りは SEC が公式に求めているやり方である(SEC のページ「Accessing EDGAR Data」)。

- 連絡先はユーザーの Gmail アドレスで、環境変数 `GMAIL_ADDRESS` に入っている(261115 にユーザーが許可)。PC では WSL の `~/.profile`、クラウドのセッションではクラウド環境「Default」の環境変数にある。
- 開き方: `curl -L -A "<リポジトリ名> $GMAIL_ADDRESS" <URL>`。SEC のページは別の場所へ移されることがあるので `-L` を付ける。
- アドレスそのものは、コマンドにも、ファイルにも、報告にも書かない。値を表示しない。
- ブラウザのふりをする名乗りは使わない。
- Codex の走行で使うには、そのリポジトリの GitHub Secrets に `GMAIL_ADDRESS` を登録し、ワークフローから Codex に渡す(note-writing では済んでいる)。

なぜ: 261115 に、連絡先を名乗らずに開いて 403 で断られた。名乗りを付けると、PC、クラウドのセッション、note-writing の Codex の走行のどれでも 200 で開けることを確かめた。クラウドの Claude は、この方法が note-writing の `docs/ノウハウ集.md` にしか書かれていなかったので読まずに試し、403 で止まった。どのリポジトリのセッションでも必ず目に入るよう、共通ルールに置く。
