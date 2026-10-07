# 教科書独学Wiki テンプレート

教科書を独学するとき、**質問とその答えをwikiとして自動で蓄積してくれるフォルダ**のテンプレートです。
[Claude Code](https://claude.com/claude-code) で開いて使います。

## 使い方

1. GitHubで **Use this template** から、教科書ごとに新しいrepoを作る（または本フォルダをコピーする）。
2. 教科書のPDFがあれば `raw/` に入れる（なくてもOK）。`index.md` に書名を記入。
3. このフォルダでClaude Codeを起動し、教科書について質問する。スクリーンショットを貼ってもよい。
4. AIが答え、質問と答えを `wiki/concepts/` の概念ページに保存し、`index.md` を更新する。
5. しばらく経ったら `/lint` でwikiを点検・整理する。

## 構成

```
raw/            教科書PDF（読み取り専用）
wiki/
  concepts/     概念ごとのページ（Q&Aを蓄積）
  log.md        更新履歴
index.md        wikiの目録（AIが毎回更新）
CLAUDE.md       AIへの運用ルール
.claude/skills/lint/   /lint スキル
```

## 設計メモ

- 質問時、AIはまず `index.md` を読んで関連ページを探す。数百ページ規模まではRAG基盤なしで十分機能する。
- スクリーンショットは保存せず、図・式の内容と論点をテキスト化して記録する。
- `/lint` は矛盾・古い記述・孤立ページ・未作成の概念・相互参照の欠落・index不整合を点検し、次に調べるべき問いを提案する。
- 運用ルールを変えたいときは `CLAUDE.md` を編集する。
