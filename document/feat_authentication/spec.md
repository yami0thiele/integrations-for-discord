# Discord認証

## 目的
「Discordでログイン」を実装する。

## 画面
![画面遷移図](./feat_authntication.svg)

## 詳細

### フロー図
![フロー図](./feat_authntication.svg)

### 1-1: ログイン画面
「Discordでログイン」以外のログイン方法は提供しないものとする。(そもそもこのサービスはDiscordを利用していることを前提としている。)

ログインボタンの押下時の処理は以下の通り:
- 認可サーバーに対してリクエストを送信
  - response_type: code
  - client_id: xxx
  - redirect_url: /login/oauth-callback
  - scope: guilds guilds.members.read identify
  - state: 発行した値
  - prompt: none
- 認可サーバーからのレスポンスを元にリダイレクトする

### 2-1: リダイレクト先 (利用許可承認画面からのcallback)
処理が完了するまではローディング表示を行う。

この画面で行うことは以下の通り:
- state 値がユーザーのセッションと対応したものであることを確認する。
- token, reflesh_token, expires, user.id を取得し、かわりにクライアント向けのトークンを発行してクライアントに渡す。(JWS)
- サーバーからエラーを受け取った場合は2-2に遷移する
  
### 2-2: エラー表示
エラーを表示して終了

