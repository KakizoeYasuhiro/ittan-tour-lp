# 一旦、ツアーで。2026 LP — ittan-tour.com デプロイ手順

中身: `index.html` / `kv.jpg` / `CNAME`(ittan-tour.com 設定済み)

## 1. GitHubへpush(Claude Code / ターミナル、約2分)

```bash
cd <このフォルダ>
git init && git add . && git commit -m "ittan tour LP"
gh repo create ittan-tour-lp --public --source=. --push
```

リポジトリ Settings → Pages → Branch: main / (root) で有効化。
CNAMEファイル同梱のためカスタムドメインは自動で `ittan-tour.com` に設定される
(反映されない場合は Custom domain 欄に手入力して Save)。

## 2. お名前.com側のDNS設定

お名前.com Navi → ネームサーバー設定 → DNSレコード設定
(対象ドメインのネームサーバーが「お名前.comのネームサーバー」= dnsv.jp系である前提)

| 種別 | ホスト名 | VALUE |
|---|---|---|
| A | (空欄) | 185.199.108.153 |
| A | (空欄) | 185.199.109.153 |
| A | (空欄) | 185.199.110.153 |
| A | (空欄) | 185.199.111.153 |
| CNAME | www | <GitHubユーザー名>.github.io |

- 既存のデフォルトレコードがあれば削除してから追加
- 転送Plus等の有料オプションは不要
- 反映は数分〜最大24時間

## 3. HTTPS有効化

DNS反映後、リポジトリ Settings → Pages で DNS check が通ったら
「Enforce HTTPS」にチェック(証明書発行に数分〜1時間程度)。

## 4. 動作確認

```bash
dig ittan-tour.com +noall +answer -t A   # 185.199.108-111.153 が返ればOK
```

https://ittan-tour.com/ を開いて表示確認。
OGPは設定済みなので、LINE/Xにリンクを貼るとキービジュアル付きカードで展開される。

## 推奨(任意): ドメイン検証

GitHub 個人 Settings → Pages → Add a verified domain で
TXTレコード検証をしておくと、サブドメイン乗っ取り対策になる。

## 更新フロー

以後は `index.html` を編集して push するだけで本番反映。
