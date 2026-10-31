# claude-common-rules

Claude Code がどのリポジトリで動くときにも守る、共通の決まりを置くリポジトリである。
ローカルの `~/.claude/` にあった古い規律のうち、今も正しく、特定の仕組みに縛られないものだけを選んで移した(261031)。

## 読み込まれ方

各プロジェクトのリポジトリの `.claude/rules/common/` にこのリポジトリの中身を置くと、Claude Code がそのプロジェクトで起動するたびに全ファイルを読み込む。ローカルの PC でもクラウドのセッションでも同じように効く。リポジトリに入っているファイルだけが読み込まれ、ローカルの `~/.claude/` は使わない。

## 取り込み方(git subtree)

初回:

```bash
git subtree add --prefix=.claude/rules/common https://github.com/tiezox/claude-common-rules.git master --squash
```

更新を取り込む:

```bash
git subtree pull --prefix=.claude/rules/common https://github.com/tiezox/claude-common-rules.git master --squash
```

## 書き方

- 平易な日本語で書き、独自の略号や造語を作らない。
- 1ファイルに1つの主題を置く。
- 決まりごとに「なぜ」を添える。理由が無い決まりは守られないためである。
- 特定のプロジェクト・特定の道具(tmux、特定のアプリ、特定の hook)に縛られる決まりはここに入れず、そのプロジェクトのリポジトリに置く。
