# Windows環境でのプロジェクトセットアップ手順

## 前提条件

以下のソフトウェアをインストールする必要があります：

1. [Docker Desktop for Windows](https://www.docker.com/products/docker-desktop)
2. [Visual Studio Code](https://code.visualstudio.com/)
3. [Git for Windows](https://gitforwindows.org/)

## セットアップ手順

### 1. Docker Desktopのインストールと設定

1. Docker Desktopをダウンロードしてインストール
2. インストール後、Docker Desktopを起動
3. WSL 2（Windows Subsystem for Linux 2）のインストールを求められた場合は、指示に従ってインストール

### 2. プロジェクトのクローン

1. PowerShellまたはコマンドプロンプトを開く
2. 任意のディレクトリに移動し、以下のコマンドを実行：

```bash
git clone https://github.com/6051-shintoku/msdocs-fastapi-postgres-codespace.git
cd msdocs-fastapi-postgres-codespace
```

### 3. Visual Studio Codeでプロジェクトを開く

1. VS Codeを起動
2. 以下の拡張機能をインストール：
   - Docker
   - Dev Containers
   - PostgreSQL

### 4. Dev Containerでプロジェクトを開く

1. VS Codeのコマンドパレット（Ctrl+Shift+P）を開く
2. `Dev Containers: Open Folder in Container`を選択
3. クローンしたプロジェクトフォルダを選択

これにより、以下の環境が自動的に構築されます：
- Python 3.11の開発環境
- PostgreSQL データベース
- 必要なPythonパッケージ

### 5. データベース接続の確認

Dev Container起動後、以下のコマンドでPostgreSQLに接続できます：

```bash
psql -h localhost -U admin -d postgres
```

パスワード（LocalPasswordOnly）を入力してログインします。

### 6. サンプルデータの確認

データベースに接続後、以下のコマンドでテーブルとデータを確認できます：

```sql
-- テーブル一覧の表示
\dt;

-- restaurantsテーブルの内容確認
SELECT * FROM restaurants;
```

## トラブルシューティング

### Docker Desktopの設定確認

1. Docker Desktopが正常に起動していることを確認
2. タスクトレイのDockerアイコンが緑色になっていることを確認
3. メモリ割り当ては最低4GB推奨（Settings > Resources > Memory）

### ポートの競合が発生する場合

- PostgreSQLのデフォルトポート（5432）が既に使用されている場合は、`.devcontainer/docker-compose.yaml`のポート設定を変更してください。

### データベース接続エラーが発生する場合

1. コンテナが正常に起動していることを確認：
```bash
docker ps
```

2. データベースのログを確認：
```bash
docker-compose logs db
```

## 補足情報

- このプロジェクトはGitHub Codespacesと互換性のある設定になっています
- ローカルのDocker環境でも同じ開発環境を再現できます
- VS CodeのDev Containers機能により、チーム全員が同じ開発環境を使用できます

## 参考リンク

- [Docker Desktop Documentation](https://docs.docker.com/desktop/windows/)
- [Visual Studio Code Dev Containers](https://code.visualstudio.com/docs/devcontainers/containers)
- [PostgreSQL Documentation](https://www.postgresql.org/docs/)