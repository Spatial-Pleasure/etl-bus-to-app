# ETL Bus to App

## 概要

DWH（BigQuery）から Spatial Pleasure アプリへデータを転送する ETL プロセスを実装するプログラム。

## 機能

- BigQuery からのデータ抽出
- ローカルデータの変換処理
- アプリケーション DB へのデータ投入
- スケジュール実行機能

## ディレクトリ構成

project_root/
├── notebooks/ # 検証用 Jupyter ノートブック
│ ├── data_validation/ # データ検証用
│ └── transformation_test/ # 変換ロジック検証用
│
├── src/ # 本番用ソースコード
│ ├── **init**.py
│ ├── config/ # 設定ファイル
│ │ ├── **init**.py
│ │ └── settings.py
│ │
│ ├── transformers/ # データ変換ロジック
│ │ ├── **init**.py
│ │ └── data_transformer.py
│ │
│ ├── utils/ # ユーティリティ関数
│ │ ├── **init**.py
│ │ └── file_handler.py
│ │
│ └── main.py # メインスクリプト
│
├── data/ # データディレクトリ
│ ├── raw/ # 元データ
│ ├── interim/ # 中間生成物
│ └── processed/ # 変換後データ
│
├── tests/ # テストコード
│ ├── **init**.py
│ └── test_transformer.py
│
├── .gitignore
├── README.md
├── requirements.txt
└── setup.py

## ディレクトリの説明

notebooks/:

- データの検証や変換ロジックの試行錯誤を行うための場所
- 実験的なコードをここで検証し、確定したロジックを src/に移植

src/:

- 本番用のコードを配置
- モジュール化された構造で保守性を確保
- 設定、変換ロジック、ユーティリティを分離

data/:

- データの流れを明確に分離（raw → interim → processed）
- .gitignore でデータファイルを管理対象外に設定可能

tests/:

- 変換ロジックのユニットテストを配置
- CI での自動テストを実現

## システム要件

- Python 3.x
- Google Cloud SDK
- 必要な Python パッケージ
  - google-cloud-bigquery
  - pandas
  - sqlalchemy
  - etc...

## セットアップ手順

1. 環境構築
2. 認証設定
3. 設定ファイルの準備

## 使用方法

1．開発環境の起動
```
# コンテナの起動
docker-compose up -d etl-dev

# Jupyter Labを必要なときに起動
docker-compose exec etl-dev jupyter lab --ip 0.0.0.0 --port 8888 --no-browser --allow-root --NotebookApp.token=''

# コンテナ内でコマンドを実行
docker-compose exec etl-dev bash
```
2. 本番環境のテスト
```
# ETL処理の実行
docker-compose up etl-prod
```

## 設定

- 環境変数の説明
- 設定ファイルのパラメータ説明

## ETL プロセスの詳細

1. データ抽出（Extract）

   - BigQuery からのデータ取得方法
   - 対象テーブル・クエリの説明

2. データ変換（Transform）

   - データクレンジング
   - データ形式の変換
   - ビジネスロジックの適用

3. データ投入（Load）
   - アプリケーション DB への書き込み
   - エラーハンドリング

## スケジュール実行

- Cron 設定
- 実行間隔
- ログ管理

## エラーハンドリング

- エラーパターン
- リトライ処理
- 通知設定

## モニタリング

- ログ形式
- メトリクス
- アラート設定

## トラブルシューティング

よくある問題と解決方法

## 貢献方法

プロジェクトへの貢献手順

## ライセンス

ライセンス情報
