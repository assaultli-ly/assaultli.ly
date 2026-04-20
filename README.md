# assaultli.ly

アサルトリリィ（Assault Lily）関連のリンクをまとめた、シンプルでモダンな非公式ポータルサイトです。

🌐 **Website:** [https://assaultli.ly](https://assaultli.ly)

## 📖 概要

このプロジェクトは、Vue.jsとTailwind CSSを使用して構築されています。  
すべてのリンクデータは単一のYAMLファイル（[`src/data/links.yaml`](https://github.com/assaultli-ly/assaultli.ly/blob/main/src/data/links.yaml)）で管理されており、データを更新するだけでサイトが自動的に構築・公開（Cloudflare Pages）される仕組みになっています。

## 🤝 リンク追加のお願い (Contributing)

本サイトはコミュニティベースで運用しています。新しい関連リンクの追加や、既存リンクの修正案をいつでも歓迎しています！

### おすすめ：Issueで依頼する（最も簡単です）

Gitの操作に慣れていない方でも、簡単にリンクの追加依頼ができます。

1. [Issuesページ](https://github.com/assaultli-ly/assaultli.ly/issues/new) にアクセスします（※GitHubアカウントが必要です）。
2. タイトルに「〇〇のリンク追加希望」と入力します。
3. 本文に、追加したいサイトの**タイトル**と**URL**を書いて送信してください。
4. 管理者が確認し、サイトに反映させます。

### 開発者向け：Pull Requestを送る
ご自身でYAMLファイルを編集し、直接リポジトリに変更を提案していただくことも大歓迎です。

1. このリポジトリを Fork します。
2. `src/data/links.yaml` にリンク情報を追記・修正します。
3. 変更を Commit & Push し、このリポジトリに向けて Pull Request を作成してください。

## 🛠 ローカル開発環境のセットアップ

手元の環境でデザインの変更や動作確認を行いたい場合は、以下のコマンドで開発サーバーを起動できます。

```bash
git clone https://github.com/assaultli-ly/assaultli.ly.git
cd assaultli.ly
npm install
npm run dev
```

## ⚠️ 免責事項

本サイトおよび本リポジトリは、個人による非公式のファンプロジェクトであり、各権利者様とは一切関係ありません。
