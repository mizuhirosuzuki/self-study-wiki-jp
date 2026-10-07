# 教科書独学Wiki テンプレート

教科書を独学するとき、**質問とその答えをwikiとして自動で蓄積してくれるフォルダ**のテンプレートです。
[Claude Code](https://claude.com/claude-code) で開いて使います。

## 使い方

1. GitHubで **Use this template** から、教科書ごとに新しいrepoを作る（または本フォルダをコピーする）。
2. 教科書のPDFがあれば `raw/` に入れる（なくてもOK）。`index.md` に書名を記入。
3. このフォルダでClaude Codeを起動し、教科書について質問する。スクリーンショットを貼ってもよい。
4. AIが答え、質問と答えを `wiki/concepts/` の概念ページに保存し、`index.md` を更新する。
5. しばらく経ったら `/lint` でwikiを点検・整理する。

## テンプレートとして使う手順

このrepoはGitHubの **Template repository** に設定済みです。教科書ごとに、次の手順で新しいrepoを作ります。

1. GitHubのこのrepoのページ右上の緑のボタン **Use this template** → **Create a new repository** を選ぶ。
2. **Owner** と **Repository name**（例: `wiki-<教科書名>`）を入力する。教科書の内容を含むなら **Private** を推奨。**Create repository** を押す。
3. 作成したrepoをcloneして、そのフォルダに移動する。

   ```bash
   git clone https://github.com/<ユーザー名>/<新しいrepo名>.git
   cd <新しいrepo名>
   ```

4. `index.md` の冒頭に書名・著者・版を記入する。PDFがあれば `raw/` に入れる。著作権のあるPDFをpushしたくない場合は、`.gitignore` の `# raw/*.pdf` のコメントを外す。
5. そのフォルダでClaude Codeを起動し、教科書について質問する（上の「使い方」の3以降）。
6. wikiへの変更は、通常どおり `git commit` と `git push` で保存する。

補足: **Use this template** は、コピー元のコミット履歴を引き継がない新規repoを作ります（fork とは異なります）。

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
