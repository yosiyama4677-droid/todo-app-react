# Todoアプリ DB設計書

## 1. 概要

本ドキュメントでは、Todoアプリで使用するデータベース設計について定義する。

### 対象機能

* Todo一覧取得
* Todo詳細取得
* Todo作成
* Todo更新
* Todo削除

---

## 2. ER図

### 現在の構成

```text
┌─────────────────────┐
│       todos         │
├─────────────────────┤
│ id (PK)             │
│ title               │
│ completed           │
│ created_at          │
│ updated_at          │
└─────────────────────┘
```

---

## 3. テーブル定義

### todos

| カラム名       | 型            | NULL     | デフォルト値            | 説明      |
| ---------- | ------------ | -------- | ----------------- | ------- |
| id         | INT          | NOT NULL | AUTO_INCREMENT    | TodoID  |
| title      | VARCHAR(255) | NOT NULL | -                 | Todoの内容 |
| completed  | BOOLEAN      | NOT NULL | FALSE             | 完了状態    |
| created_at | TIMESTAMP    | NOT NULL | CURRENT_TIMESTAMP | 作成日時    |
| updated_at | TIMESTAMP    | NOT NULL | CURRENT_TIMESTAMP | 更新日時    |

---

## 4. CREATE TABLE

```sql
CREATE TABLE todos (
    id INT AUTO_INCREMENT PRIMARY KEY,
    title VARCHAR(255) NOT NULL,
    completed BOOLEAN NOT NULL DEFAULT FALSE,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
        ON UPDATE CURRENT_TIMESTAMP
);
```

---

## 5. APIとDBの対応

### GET /todos

#### 概要

Todo一覧を取得する。

#### SQL

```sql
SELECT *
FROM todos
ORDER BY id;
```

#### レスポンス例

```json
[
  {
    "id": 1,
    "title": "買い物",
    "completed": false
  },
  {
    "id": 2,
    "title": "筋トレ",
    "completed": true
  }
]
```

---

### GET /todos/{id}

#### 概要

指定したTodoを取得する。

#### SQL

```sql
SELECT *
FROM todos
WHERE id = ?;
```

#### レスポンス例

```json
{
  "id": 1,
  "title": "買い物",
  "completed": false
}
```

---

### POST /todos

#### 概要

Todoを新規作成する。

#### リクエスト

```json
{
  "title": "散歩する"
}
```

#### SQL

```sql
INSERT INTO todos (
    title
)
VALUES (
    ?
);
```

#### レスポンス例

```json
{
  "id": 3,
  "title": "散歩する",
  "completed": false
}
```

---

### PUT /todos/{id}

#### 概要

Todoを更新する。

#### リクエスト

```json
{
  "title": "散歩する",
  "completed": true
}
```

#### SQL

```sql
UPDATE todos
SET
    title = ?,
    completed = ?
WHERE id = ?;
```

#### レスポンス例

```json
{
  "id": 3,
  "title": "散歩する",
  "completed": true
}
```

### DELETE /todos/{id}

#### 概要
指定したTODOを削除する。

### SQL
```SQL
DELETE FROM todos
WHERE id = ?;
```

---

## 6. Expressとの対応表

| API               | SQL          | Express               |
| ----------------- | ------------ | --------------------- |
| GET /todos        | SELECT       | app.get('/todos')     |
| GET /todos/:id    | SELECT WHERE | app.get('/todos/:id') |
| POST /todos       | INSERT       | app.post('/todos')    |
| PUT /todos/:id    | UPDATE       | app.put('/todos/:id') |
| DELETE /todos/:id | DELETE       | app.delete('/todos/') |
---

## 7. 今後の拡張案

### 未定

---

## 8. まとめ

本設計では、Todoアプリの基本機能を実現するために `todos` テーブルを定義した。

この設計を基に、ExpressとMySQLを用いたTodo APIの実装を行う。
