# 環境構築手順書

## 前提条件
以下がダウンロードされていること
  - Docker
  - node.js

## 環境構築手順

#### 1. 環境設定フォルダをダウンロードする
  ```
  $ git clone https://github.com/hr502/bs-attendance.git
  ```
  
#### 2. 上記でダウンロードしたフォルダ内に移動し、起動に必要なファイルを作成、またはインストールする。
  - backendの設定
    ```
    $ cd ~/[任意のバス]/bs-attendance/backend/src
    $ composer install
    $ cp .env.example .env
    $ php artisan key:generate
    ```

  - frontendの設定
    ```
    $ cd ~/[任意のバス]/bs-attendance/frontend/src
    $ yarn install
    ```
  
#### 3. コンテナをビルドする
  ~~~
  $ cd ~/[任意のバス]/bs-attendance
  $ docker compose build 
  ~~~

#### 4. コンテナを起動する
  ~~~
  $ docker compose up -d
  ~~~
    
#### 5. 接続を確認する
  - `http://localhost:8080` にアクセスしLaravelの初期画面が表示されること
  
  - `http://localhost:3000` にアクセスしnext.jsの初期画面が表示されること
  
#### 6. DB接続設定(pgAdmin4の場合)
  サーバを以下の設定で登録する
  - Generalタブ
    - 名前: [任意]
  - 接続タブ
    - ホスト名/アドレス: 127.0.0.1
    - ポート番号: 5432
    - 管理用データベース: postgres
    - ユーザ名: postgres
    - パスワード: postgres

#### 7. マイグレーション実行
  - コンテナに入る
    ~~~
    // (コンテナを起動している状態で)
    $ docker compose exec app bash
    ~~~
  
  - マイグレーションを行う
    ~~~
    $ php artisan migrate
    ~~~
    
#### 8.DB接続確認(pgAdmin4の場合)
  - `Servers > [6で設定した名前] > bs > スキーマ > public > テーブル` 以下に
    マイグレーション内容と同様のテーブルが作成されていることを確認する。
