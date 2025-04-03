---
title:  "[Client - Readme(JPN)] DataX Project "
categories: [Project, Personal]
tags:
  [node.js,
  vue.js,
  aws,
  ngnix,
  ] 
image: "/assets/img/title/vue.png"
---

# ~~-- Cors エラー未解決~~ -> 25.03.10 解決
サーバー側でまだCorsエラーが解決されていないため、Corsチェックを行わないブラウザでのみアクセス可能です。

[Safari 開発者モードでCORSを無効化する方法]
1. Safariを開く
2. "開発者モード" を有効化
    * 上部メニューの Safari → 設定(Preferences) → 詳細(Advanced) をクリック
    * "メニューバーに開発メニューを表示(Show Develop menu in menu bar)" をチェック
3. 開発メニューからCORSを無効化
    * メニューバーで "開発(Develop) → クロスオリジン制限を無効化(Disable Cross-Origin Restrictions)" をクリック

# プロジェクト概要
このプロジェクトは、Ruby on RailsとVue.jsを使用して実装されたブログプラットフォームです。ユーザー認証、記事管理、検索フィルタリングなどの機能を含みます。

[Server Github](https://github.com/SonMyeongJin/DataX_Project_Server-)


~~[デプロイ済み]~~
http://54.180.239.200

## 開発環境
- 開発環境: macOS
- Node.js: 23.9.0
- Vue.js: 3.5.13
- デプロイ: AWS EC2, Nginx

# プロジェクトのセットアップ手順

- 開発フロー
    1. JWTトークンを使用するためにAxiosを設定
    2. ログインページの実装
    3. ユーザー登録ページの実装
    4. 記事の作成・詳細ページの実装
    5. カテゴリーと検索機能の追加
    6. 記事の削除・編集を実装 (作成者のみ削除可能)
    7. タグを利用した記事移動の実装
    8. UIの調整
    9. AWSとNginxを利用したデプロイ
    10. Railsサーバーと接続

# 実装した機能

- ログイン・ログアウトの状態
    - ログイン状態によって表示画面が変化します。
    - PostListページはログアウト状態でも閲覧可能ですが、記事の作成ページはログイン時のみアクセス可能（トークンの確認が必要）。

- 記事の編集・削除ボタンは作成者のみ有効
    - ログインユーザーのuser_idと記事作成者のuser_idが一致する場合のみ、編集・削除ボタンが表示されるように実装。
    - ![](/assets/img/posts/post/datax_post.jpeg)

- カテゴリーおよび検索ボックスを利用した検索機能
    - PostListページでカテゴリーを選択すると、同じカテゴリーの記事がフィルタリングされます。
    - 検索ボックスでは、タイトルや内容に検索ワードが含まれる記事を表示。

- タグ機能
    - PostDetailページでタグをクリックすると、同じタグを持つ記事を一覧表示。
    - 記事作成時にタグはカンマ区切りで入力し、サーバーへ配列として送信。
    例: タグ1,タグ2 -> ["タグ1", "タグ2"]

- モバイル版UI
    - 画面サイズが768px以下の場合、メニューバーがモバイル向けのデザインに変更。
     - ![](/assets/img/posts/post/datax_mobile.gif)
