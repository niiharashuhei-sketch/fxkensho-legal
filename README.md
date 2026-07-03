# MyBacktest 法務・サポートページ（静的サイト）

App Store / Google Play 審査で必須のプライバシーポリシーURL・利用規約URLを公開するための
静的HTMLサイト。**このリポジトリ（アプリ本体）はprivateのままでよい** — GitHub Pagesの
カスタムドメインは無料プランではpublicリポジトリでのみ使えるため、このフォルダの中身だけを
別の新規public GitHubリポジトリへコピーして公開する。

## 内容
- `index.html` — トップページ（アプリ紹介＋各ページへのリンク）
- `privacy/index.html` — プライバシーポリシー（`/privacy/` で表示）
- `terms/index.html` — 利用規約（`/terms/` で表示）
- `style.css` — 共通スタイル
- `CNAME` — カスタムドメイン指定（`legal.mybacktest.app`）

本文はアプリ内 `lib/presentation/widgets/support/legal_texts.dart` の
`kTermsOfServiceText` / `kPrivacyPolicyText` と同一内容（HTML化のみ）。
**アプリ内の文言を変更したら、このサイトの該当ページも手動で同期すること**
（二重管理・自動同期の仕組みは無し＝v1では簡易対応）。

## 公開手順
1. GitHubで新しい**public**リポジトリを作成（例: `mybacktest-legal`）。
2. このフォルダの中身一式をそのリポジトリのルートに配置してpush
   （またはGitHub Webの「Add file → Upload files」でドラッグ&ドロップ）。
3. リポジトリの Settings → Pages → Source を `main` ブランチ / `root` に設定。
4. 同じ Pages 設定画面の Custom domain に `legal.mybacktest.app` を入力して保存
   （`CNAME` ファイルがあるので自動検出される）。
5. ドメインのDNS管理画面（Google Workspace経由なら admin.google.com →
   アカウント → ドメイン → DNSレコードを管理）で以下を追加:
   - 種別: CNAME
   - ホスト: `legal`
   - 値: `<GitHubユーザー名>.github.io`
6. 反映を待ってから（数分〜数時間）Pages設定画面で「DNS check successful」を確認し、
   「Enforce HTTPS」を有効化。
7. `https://legal.mybacktest.app/privacy/` と `/terms/` が正しく表示されることを確認。
8. App Store Connect / Google Play Console のプライバシーポリシーURL欄に
   `https://legal.mybacktest.app/privacy/` を登録する。

## 制定日について
2026-07-03（このページ作成日）を暫定の制定日として記載済み。実際のストア提出日が
これと異なる場合は、`privacy/index.html` と `terms/index.html` の
`制定日：2026年7月3日` を実際の公開日に書き換えること。
