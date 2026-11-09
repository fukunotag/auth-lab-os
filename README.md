# Auth Lab OS · GitHub Pages edition

## この版について
既存Auth Lab OSのデスクトップUIと既存アプリを維持し、GitHub Pages向けに静的サイトとして公開できる形にした学習用プロトタイプです。API Manager、ブラウザAPI機能検出、追加認証方式のアプリ一覧を追加しています。

### 実装済み
- 既存 Password / PIN / Pattern / Image / Rhythm / TOTP のローカル実験
- Auth Builder / Auth Compare / Settings
- API Manager：Secure Context、WebAuthn、Web Crypto、Camera/Microphone、Geolocation、NFC、Bluetooth、USBの機能検出
- カメラ・マイク・位置情報の許可テスト（利用後ストリーム停止、座標は保存しない）
- LocalStorageによるブラウザ内保存
- 追加方式の独立アプリ枠（未実装分はシミュレーション・学習ノート）

## GitHub Pagesへのデプロイ
1. GitHubにサインインし、New repositoryで `auth-lab-os` などのリポジトリを作成する。公開範囲は用途に合わせて選ぶ。GitHub FreeではPages公開対象リポジトリの公開条件に注意。
2. このZIPを展開し、`index.html` と `README.md` をリポジトリの最上位に置く。`Code.gs.txt` はGitHub Pagesでは使用しない。
3. GitHubのリポジトリ画面で **Add file → Upload files** を選び、ファイルをアップロードして **Commit changes**。またはGitHub DesktopでフォルダをPublishする。
4. リポジトリの **Settings → Pages** を開く。
5. **Build and deployment → Deploy from a branch** を選ぶ。
6. Branchを `main`、Folderを `/(root)` にしてSave。
7. 数分待ち、Pages欄に表示された `https://ユーザー名.github.io/リポジトリ名/` を開く。
8. Settings → PagesでHTTPSが有効であることを確認する。GitHub PagesはHTTPS配信に対応する。

## 更新方法
`index.html` を編集してGitHubへ再アップロードし、Commit changesする。Pagesが自動で再デプロイする。

## Google Sheets / GASについて
- `Code.gs.txt` は以前のGAS保存機能の参考コード。Apps Scriptプロジェクトに貼り付けて使う。
- このGitHub Pages版から `google.script.run` は利用できないため、GAS同期ボタンはGAS内で開いた場合に限り動作する。GitHub PagesからSheetsへ直接つなぐ安全な同期は、この版にはまだ実装していない。
- GitHub Pagesは静的ホスティングで、サーバー側コードや秘密情報を安全に保管できない。APIキーやクライアントシークレットをHTML/JavaScriptへ書かないこと。
- Sheets同期を後で追加する場合は、認証・アクセス制御を設計したバックエンドまたはOAuthを介す。公開GAS Web Appを無認証の書き込みAPIとして公開しない。

## Passkey / WebAuthnについて
- API ManagerはWebAuthn APIの有無を検出するだけで、Passkeyの登録・認証を完了しない。
- 本物のWebAuthnにはRP IDとOriginの整合、サーバーが発行する一回限りのチャレンジ、署名検証、credential管理が必要。GitHub Pages単独ではサーバー検証を実装できない。
- 端末の指紋・顔認証データをページが読み取ることはできない。対応する端末認証器に本人確認を委ねる。

## セキュリティ・プライバシー
- 実在アカウントのパスワード、PIN、OTP秘密鍵、個人情報を入力しない。すべて架空の実験値を使う。
- LocalStorageは暗号化された秘密保管庫ではない。同じブラウザープロファイルから読み取れるため、機密情報を保存しない。
- 生体データは取得・保存しない。カメラ/マイクは明示的な操作で許可を求め、テスト後にストリームを停止する。
- 追加アプリの多くは現時点ではシミュレーション枠であり、実認証機能ではない。

## ファイル
- `index.html`：GitHub Pagesで公開する本体
- `Code.gs.txt`：既存GAS保存機能の参考コード（GitHub Pagesでは不要）
- `README.md`：この説明
