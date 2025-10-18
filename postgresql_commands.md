# PostgreSQLの基本的なコマンド

## データベース接続

```bash
# バージョン確認
psql --version

# データベースへの接続
psql -h localhost -U admin -d postgres
# -h: ホスト名
# -U: ユーザー名
# -d: データベース名
```

## よく使うpsqlコマンド

### テーブル関連

```sql
-- テーブル一覧の表示
\dt;

-- テーブルの構造確認
\d テーブル名;
例: \d restaurants;

-- 全てのレコードを表示
SELECT * FROM テーブル名;
例: SELECT * FROM restaurants;
```

### その他の便利なコマンド

```sql
-- ヘルプの表示
\help または \?

-- データベース一覧
\l

-- スキーマ一覧
\dn

-- ユーザー一覧
\du

-- psqlの終了
\q または quit
```

## サンプルの実行結果

```sql
postgres=# \dt;
          List of relations
 Schema |    Name     | Type  | Owner 
--------+-------------+-------+-------
 public | restaurants | table | admin
(1 row)

postgres=# select * from restaurants;
 id |          name          |       address        
----+------------------------+----------------------
  1 | 振徳レストラン         | 日南市板敷４１０番地
  2 | 飫肥城下祭りレストラン | 日南市飫肥1234番地
  3 | 飫肥城下祭りレストラン | 日南市飫肥1234番地
  4 | レストラン             | 日南1234番地
(4 rows)
```

## 一般的なSQLコマンド

```sql
-- レコードの挿入
INSERT INTO restaurants (name, address) 
VALUES ('レストラン名', '住所');

-- レコードの更新
UPDATE restaurants 
SET name = '新しい名前' 
WHERE id = 1;

-- レコードの削除
DELETE FROM restaurants 
WHERE id = 1;

-- 特定のカラムのみ選択
SELECT name, address 
FROM restaurants;

-- 条件付き検索
SELECT * 
FROM restaurants 
WHERE name LIKE '%レストラン%';
```

## 注意点

- コマンドは大文字・小文字を区別しません（ただし、値は区別します）
- SQLコマンドは必ずセミコロン(;)で終える必要があります
- テーブル名やカラム名に日本語を使用する場合は、ダブルクォーテーション(")で囲む必要があります
- バックスラッシュコマンド（\dなど）にはセミコロンは不要です