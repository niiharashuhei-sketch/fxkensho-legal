# アプリ内お知らせ（notice.json）の使い方

MyBacktest アプリは起動時とフォアグラウンド復帰時に
`https://legal.mybacktest.app/notice.json` を取得し、お知らせを表示します
（重大＝閉じるまで消えないダイアログ／注意・情報＝画面上部のバナー）。

## 緊急メッセージを出す手順

1. このリポジトリの `notice.json` を編集（GitHubのWeb上で鉛筆アイコン→編集→Commitでも可）
2. push / Commit すると GitHub Pages が1〜2分で自動デプロイ
3. ユーザーのアプリに次回起動時・復帰時に表示される

## 書式

```json
{
  "notices": [
    {
      "id": "2026-07-17-dl-outage",
      "severity": "critical",
      "title": {"ja": "データ取得障害のお知らせ", "en": "Data download outage"},
      "body": {
        "ja": "現在、相場データのダウンロードに障害が発生しています。復旧までしばらくお待ちください。",
        "en": "Market data downloads are currently experiencing an outage. Please wait for recovery."
      },
      "minVersion": "1.0.0",
      "maxVersion": "1.0.1",
      "url": "https://legal.mybacktest.app/"
    }
  ]
}
```

- `id` **必須・一意**。ユーザーの既読管理の単位（同じidは一度閉じたら再表示されない
  ＝内容を更新して再度全員に見せたいときは新しいidにする）
- `severity` **必須**: `critical`（閉じるまで消えないダイアログ）/ `warn` / `info`（上部バナー）
- `title.ja` **必須**。`en`・`body`・`url` は任意（en が無ければ ja を表示）
- `minVersion` / `maxVersion` 任意: 対象アプリバージョンの範囲（例: 旧バージョンだけに表示）
- 取り下げ＝ `"notices": []` に戻して Commit

## 注意

- JSONの文法エラー（カンマ忘れ等）があるとアプリ側は**黙って全件スキップ**します
  （アプリを壊さない安全設計）。編集後は https://legal.mybacktest.app/notice.json を
  ブラウザで開いて表示されるか確認すること
- アプリは取得のみで何も送信しません
