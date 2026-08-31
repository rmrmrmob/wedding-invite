# wedding-invite — Richard & Hazuki 披露宴Web招待状

オーナー(GitHub: rmrmrmob)の披露宴のWeb招待状。LINEでゲストに
URLを配り、サインインなしで誰でも開ける。作業を続けるときはまずこのファイルを読むこと。

## 披露宴の情報

- 新郎新婦: **RICHARD & HAZUKI**
- 日時: **2026年12月13日(日) 15:30 受付開始 / 16:00 開宴 〜 19:30**
- 会場: 結婚式場 N.B.C(日本ブライダルセンター) 〒904-0021 沖縄県沖縄市胡屋6-12-1 / TEL 098-933-0808
- 那覇空港⇔会場のシャトルバス運行予定(利用希望をフォームで収集)
- 披露宴後に二次会あり(参加希望もフォームで収集)
- 出欠回答の締切: **2026年10月31日(土)**

## 公開場所(2つを常に同期させること)

1. **本番(ゲスト配布用)**: https://rmrmrmob.github.io/wedding-invite/
   - このリポジトリの `main` にpushすると GitHub Actions (`.github/workflows/deploy.yml`) が自動デプロイ
   - GitHub Pagesのキャッシュは最大10分程度
2. **プレビュー(claude.aiアーティファクト)**: https://claude.ai/code/artifact/bf01c780-1bb5-4bad-8367-9a60bb964160
   - `index.html` を編集したら、同じ変更をアーティファクトにも適用して再公開する
   - 過去に片方だけ更新して「直ってない」と混乱が起きた。**必ず両方更新**

## 出欠回答(RSVP)の仕組み

送信ボタンで **GoogleフォームへPOST(fetch no-cors)** し自動集計。オーナーはフォームの
「回答」タブ / 連携スプレッドシートで確認する。

- 送信先: `https://docs.google.com/forms/d/e/1FAIpQLScGOIkMYKBRQ-AE9gyJU7H10WpKAS4TOCMEzk3ktfj_28w7fA/formResponse`
- entry ID対応表は `index.html` の `GOOGLE_ENTRY`(attend/name/kana/side/address/tel/bus/party/allergy/message の10項目)
- 送信失敗時のフォールバック: アーティファクト保存 → それも不可ならLINEコピー方式
- Googleフォーム側は「公開」済み・「リンクを知っている全員」が回答可・メール収集なしであること

## デザイン・構成

- テーマ: アメリカンダイナー風(チェッカー柄、チェリーレッド×マスタード、Yellowtail/Alfa Slab Oneフォント)
- 単一ファイル `index.html`(CSS/JS込み)+ `ogp.jpg`(LINEプレビュー用OGP画像、お二人の写真)
- トップ写真は新郎新婦専用ボタンで設定し `#rsvp-data` のJSON(`heroPhoto`, base64)に保存済み
- 写真あり時は「披露宴のご招待」見出しを写真下部(名前の上)に表示(顔に被らないように)

## 環境の注意

- Claude Codeセッションからは egressポリシーで `rmrmrmob.github.io` や `docs.google.com` に
  接続できない。ライブ確認はオーナーのスマホでしてもらう。デプロイ成否は GitHub Actions の
  workflow run の conclusion で確認する
- リポジトリ作成・Pages有効化はオーナーがブラウザで実施済み(botトークンでは権限不足)
