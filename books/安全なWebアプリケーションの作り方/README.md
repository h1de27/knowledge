# 安全なWebアプリケーションの作り方

![](https://images-fe.ssl-images-amazon.com/images/I/41WBMf7zcML.jpg)

徳丸浩

# 1 ~ 2 セットアップ

# 3. Web セキュリティの基礎

## 3.1

- Sessionは他人から推測されないようにすることが大切。
- クッキーのDomain属性は原則として設定しない。

## 3.2

- 同一オリジンポリシー: URLのホストが一致していれば、iframeの中身にJSを使ってアクセスできる。
- クロスオリジンからの読み出しを許可するためには、HTTPレスポンスヘッダーに以下のコードを付け加える。
```
Access-Control-Allow-Origin: http://ecample.jp
```
- プリフライトリクエストの場合は、更にレスポンスヘッダーに付け加える項目が増える。
- XMLHttpRequestオブジェクトのwithCredentialsプロパティをtrueにする。
- レスポンスヘッダーとしてAccess-Controll-Allow-Credentials: true を返す。

# 4. Webアプリケーションの昨日別に見るセキュリティバグ
