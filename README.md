# SQLプラクティス問題集 問題作成ガイド

## 概要
これはDuckBIのSQL練習問題を作成・管理するためのガイドです。
GitHubからインポートして、独自の問題セットを作成できます。

## 問題の作成方法

### 1. リポジトリ内のディレクトリ構造
```
├── data/              # Parquetデータを配置
│   ├── users.parquet  # テーブルごとのデータファイル
│   └── orders.parquet
├── S-001.md
└── S-002.md
└── S-003.md
```

### 2. 問題ファイルの作成
各問題は1つのMarkdownファイル (.md) として作成します。

```markdown
---
id: "S-001"                      # 問題ID (必須・一意)
title: "ユーザー数を集計する"    # 問題タイトル (必須)
difficulty: "easy"              # 難易度 ["easy", "medium", "hard"] (必須)
tags: ["COUNT", "基本集計"]     # タグ配列 (必須)
tables:                        # 使用テーブル情報 (必須)
  - name: "users"
    description: "ユーザーテーブル"
initialSQL: "SELECT * FROM users"  # 初期表示するSQL (必須)
expectedResult: [               # 期待される実行結果 (必須)
  { "count": 100 }
]
solution: "SELECT COUNT(*) as count FROM users"  # 解答例SQL (必須)
hint: "COUNT関数を使って全行数を数えてみましょう"  # ヒント (任意)
---

-- 以下には任意の問題説明文をMarkdown形式で記載してください
usersテーブルに登録されているユーザーの総数を求めてください。

## テーブル定義
### users
| カラム名 | 型 | 説明 |
|---------|-------|---------|
| id | INT | ユーザーID |
| name | STRING | ユーザー名 |
| created_at | TIMESTAMP | 登録日時 |
```

### 3. データファイルの準備
- Apache Parquet形式でテーブルデータを作成
- ファイル名はテーブル名と同じにする（例: users.parquet）
- 各Parquetファイルは、DuckDBで自動でデータファイルをテーブルとして認識されます

