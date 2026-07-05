# 一旦、ツアーで。2026 ツアーLP

ワタナベシュウヘイ / 園木邦宝(Khore) / ヒトリルーム による全8公演ツアーの告知LP（1ページHTML）。

## 構成・デプロイ

- **本体**: `index.html`（単一ファイル。CSSは`<style>`内インライン、画像は`kv.jpg`を相対参照）
- **リポジトリ**: `KakizoeYasuhiro/ittan-tour-lp`（public）
- **ホスティング**: GitHub Pages（main / root）。**`main`にpushすると自動で本番反映**
- **公開URL**: https://ittan-tour.com/ （`CNAME`ファイルでカスタムドメイン設定）
- **ローカル**: `~/Projects/ittan`

## ドメイン / DNS

- ドメインは**お名前.com**で取得。ただし**DNSはCloudflareで管理**（2026-06-11にネームサーバーを `bowen.ns.cloudflare.com` / `joyce.ns.cloudflare.com` へ変更済み）。今後のDNS変更はCloudflareダッシュボードで行う
- DNSレコード（Cloudflare上、すべて **Proxied=オレンジ雲**）:
  - apex `ittan-tour.com` → A `185.199.108-111.153`（GitHub Pages 4本）
  - `www` → CNAME `kakizoeyasuhiro.github.io`
- **HTTPS**: ✅ 解決済み。CloudflareのUniversal SSL（Google Trust Services、subject=ittan-tour.com）で配信。SSL/TLSモード=**Full**、Always Use HTTPS=ON。
  - 経緯: GitHub PagesのLet's Encrypt発行が6時間以上停滞したため、Cloudflareを前段に挟む方式に切替えて解決した。GitHub側のEnforce HTTPSは未使用（CloudflareがTLS終端）。
  - ⚠️ Cloudflareのプロキシ(オレンジ雲)がOFF(DNS only)だとCloudflare証明書が効かずHTTPSが立たないので、レコードは必ずProxiedにすること。
  - 確認: `dig +short A ittan-tour.com @1.1.1.1`（104.x/172.67.x が返ればProxied）

## チケット状態バッジ（残り僅か / 売り切れ / 終了）

席数連動はせず、**HTMLのクラスを手動で付け外し**して切り替える方式（CSSは`index.html`内に実装済み）。

- **残り僅か**: 該当カードの`.show-head`に `<span class="status few">残り僅か</span>` を追加（赤塗りバッジ、購入ボタンは有効のまま）
- **売り切れ**: `<article class="show is-soldout">` にして、`.show-head`にバッジ `<span class="status soldout">SOLD OUT（全席予約済）</span>`、購入リンクを `<span class="buy sold">SOLD OUT（全席予約済）</span>` に差し替え（グレー無効ボタン＋カードを薄く）。バッジ・ボタンとも表記は **SOLD OUT（全席予約済）** で統一。サンプルは `_sample-soldout.html`
- **終了**: **自動切り替え**。各カードの `data-date="YYYY-MM-DD"` を `index.html` 末尾の`<script>`がJST基準で判定し、公演翌日0時から自動で終了表示（`is-ended` + バッジ「終了」+ ボタン「終了しました」、売り切れと同じグレー沈み）に切り替える。売り切れ表示より終了表示が優先される。手動でHTMLに `is-ended` を書いてもよい（JS無効環境のフォールバック。東京7.4は静的に記述済み）
- 適用状況（2026-07-05時点）: **東京 7.4 = 終了（静的記述）**、**愛知 8.8 = 売り切れ**。他は通常
- 運用: ユーザーから「○○が残り僅か／完売した」と言われたら該当カードにクラスを足してpushする。**終了表示は自動なので手動対応不要**（公演日程が変わったら `data-date` も更新すること）

## 全8公演（開演=記載時刻 / 開場=30分前）

東京7.4(NEIGHBOR) / 群馬7.5(SLOW TIME cafe) / 愛知8.8(鑪ら場) / 大阪8.9(Studio&Café Make) / 京都8.11(someno kyoto) / 福岡9.5(Music Bar Shangri-la) / 熊本9.6(tsukimi) / 渋谷10.3(shibuya gee-ge. ※TOUR FINAL)

- 主催: 『一旦、ツアーで。』事務局
- トーン: 白×黒×赤(`--accent: #d7261e`)。色味の調整は`index.html`の`:root`トークンのみで全体反映
