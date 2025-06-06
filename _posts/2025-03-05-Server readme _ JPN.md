---
title:  "[Server - Readme(JPN)] DataX Project "
categories: [Project, Personal]
tags:
  [ruby,
  rails,
  aws,
  mysql,
  ] 
image: "/assets/img/title/ruby.png"
---

# プロジェクト概要
このプロジェクトは、Ruby on RailsとVue.jsを使用して実装されたブログプラットフォームです。ユーザー認証、記事管理、検索フィルタリングなどの機能を含みます。

[Client Github](https://github.com/SonMyeongJin/DataX_Project_Client)


~~[APIデプロイ済み]~~
http://43.203.118.99:3000/
- リクエストはHTTPで受信され、レスポンスはJSON形式でHTTP Bodyに含まれて返されます。

## 開発環境
- 開発環境: macOS
- Ruby 3.2.6
- Rails 7.2.2.1
- データベース: MySQL 9.2.0
- デプロイ: AWS EC2

# プロジェクトのセットアップ手順

- プロジェクト環境のインストール
    - Ruby 3.2.6のインストール
    - Bundlerのインストール
    - データベース(MySQL)のインストール
    - Railsのインストール

- 開発フロー
    1. ERDの作成
        - ![](/assets/img/posts/post/datax_erd.png)
    2. MySQLとRailsプロジェクトの接続
    3. ERDデータに基づくモデルの定義 (属性)
    4. API明細書作成
        - ### [API Notion URL](https://son-myeongjin.notion.site/datax-project-api?v=1aa07b1a3de181e38b81000cf2237f46)

        - ![](/assets/img/posts/post/datax_notion.png)
    5. JWTトークンを使用したログイン機能の実装
        - RailsのDeviseライブラリを使用
    6. 記事の作成・削除・編集のロジックを実装
    7. タグ機能の実装
    8. AWSを利用したデプロイ
    9. Vueクライアントとの連携

# 実装した機能

- ユーザー登録
    - 名前、メールアドレス、パスワードを入力
    - 登録成功後、名前、メールアドレス、パスワードをデータベースに保存
    - レスポンス: 名前、メールアドレス、作成日、ユーザーID
    (ユーザーIDは後で記事の編集や削除時に所有者を確認するために使用)

- ログイン・ログアウト機能
    - ログイン機能
        - メールアドレスとパスワードを受け取り、データベースで認証を行う
        - 認証成功時にトークンを返す
        - トークンはHTTPヘッダーに含めることで、特定の機能(記事作成、ログアウトなど)へのアクセスが可能
    - ログアウト機能 (トークン必要)
        - トークンを確認し、ログイン状態であればログアウト成功メッセージを返す
        - システムはトークンのJTI値を特定し、ログアウトしたトークンでのリクエストを拒否する

- 記事投稿機能 (トークン必要)
    - 記事の作成
    - 記事の削除
    - 記事の編集
    - 記事リストの取得

- タグ機能
    - タグの作成
        - 記事作成時にタグを追加可能
        既存のタグがある場合、そのIDを返し、新規タグの場合は新しいIDを割り当てて返す

    - タグによるフィルタリング
        - GETリクエストでタグIDを指定すると、同じタグを持つ記事を配列で返す

    - ![](/assets/img/posts/post/datax_tag.jpeg)

# 工夫したポイント
- JTIを利用したセキュリティ強化
   - JWTトークンのみでログインを管理すると、ログアウト後もトークンが有効でアクセスが可能となるため、JTIを導入。JTIによりトークンの拒否が可能になり、セキュリティを強化しました。

- ![](/assets/img/posts/post/datax_login.jpeg)