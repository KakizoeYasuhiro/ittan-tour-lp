# 一旦、ツアーで。2026 ツアーLP

ワタナベシュウヘイ / 園木邦宝(Khore) / ヒトリルーム による全8公演ツアーの告知LP（1ページHTML）。

## 構成・デプロイ

- **本体**: `index.html`（単一ファイル。CSSは`<style>`内インライン、画像は`kv.jpg`を相対参照）
- **リポジトリ**: `KakizoeYasuhiro/ittan-tour-lp`（public）
- **ホスティング**: GitHub Pages（main / root）。**`main`にpushすると自動で本番反映**
- **公開URL**: https://ittan-tour.com/ （`CNAME`ファイルでカスタムドメイン設定）
- **ローカル**: `~/Projects/ittan`

## ドメイン / DNS

- ドメインは**お名前.com**で取得・管理（ネームサーバーもお名前.com = `dns1/dns2.onamae.com`）
- DNSレコード（設定済み・正常）:
  - apex `ittan-tour.com` → A `185.199.108-111.153`（GitHub Pages 4本）
  - `www` → CNAME `kakizoeyasuhiro.github.io`
- **HTTPS証明書**: 2026-06-11時点でGitHub側のLet's Encrypt発行が長時間（6時間以上）停滞中。DNS/CAA/ドメイン設定は正常確認済みなので原因はGitHub側。発行されれば `gh api -X PUT repos/KakizoeYasuhiro/ittan-tour-lp/pages -f https_enforced=true` でEnforce HTTPSを有効化する。急ぐ場合はCloudflareを前段に挟む案あり。
  - 確認: `gh api repos/KakizoeYasuhiro/ittan-tour-lp/pages --jq '.https_certificate.state'`

## チケット状態バッジ（残り僅か / 売り切れ）

席数連動はせず、**HTMLのクラスを手動で付け外し**して切り替える方式（CSSは`index.html`内に実装済み）。

- **残り僅か**: 該当カードの`.show-head`に `<span class="status few">残り僅か</span>` を追加（赤塗りバッジ、購入ボタンは有効のまま）。※愛知 8.8 に適用済み
- **売り切れ**: `<article class="show is-soldout">` にして、購入リンクを `<span class="buy sold">SOLD OUT（全席予約済）</span>` に差し替え（グレー無効ボタン＋カードを薄く）。売り切れ表記は **SOLD OUT（全席予約済）** で統一。本番では現状未使用。サンプルは `_sample-soldout.html`
- 運用: ユーザーから「○○が残り僅か／完売した」と言われたら、該当カードにクラスを足してpushする

## 全8公演（開演=記載時刻 / 開場=30分前）

東京7.4(NEIGHBOR) / 群馬7.5(SLOW TIME cafe) / 愛知8.8(鑪ら場) / 大阪8.9(Studio&Café Make) / 京都8.11(someno kyoto) / 福岡9.5(Music Bar Shangri-la) / 熊本9.6(tsukimi) / 渋谷10.3(shibuya gee-ge. ※TOUR FINAL)

- 主催: 『一旦、ツアーで。』事務局
- トーン: 白×黒×赤(`--accent: #d7261e`)。色味の調整は`index.html`の`:root`トークンのみで全体反映
