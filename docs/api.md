# APIエンドポイント
実装するエンドポイントを記載する。

## エンドポイント一覧
| メソッド | パス | 説明 |
|--------|------|------|
| GET | /todos/{id} | TODO詳細の取得 |
| GET | /todos  | TODO一覧の取得　|
| POST | /todos | TODOの作成　|
| PUT | /todos/{id} | TODOの更新　|
| DELETE | /todos/{id} | TODOの削除　|

## エンドポイント詳細

### GET/todos/{id}
指定されたIDのTODOを1件返す。

パスパラメータ:

| パラメータ名 | 型 | 説明 |
|------------|-----|------|
| id | integer | 取得するTODOのID |

**レスポンス(200)**
```json
{
  "id": 1,
  "title": "title",
  "description": "description",
  "done": false
}
```
**レスポンス(404)**
```json
{
  "message":"TODO not found"
}
```

### GET /todos
TODO一覧の取得

**レスポンス(200)**
```json
[
  {
    "id": 1,
    "title": "title1",
    "description": "description1",
    "done": false
  },
  {
    "id": 2,
    "title": "title2",
    "description": "description2",
    "done": true
  }
]
```

### POST /todos
TODOを作成する

リクエストボディ:
| パラメータ名 | 型 | 説明 |
|------------|-----|------|
| title | string | 作成したTODOのタイトル |
| description | string | 作成したTODOの詳細　| 

**リクエスト例**
```json
{
  "title": "買い物",
  "description": "卵を買う"
}
```

**レスポンス(201)**
```json
{
  "id": 2,
  "title": "title",
  "description": "description",
  "done": false
}
```

**レスポンス(400)**
```json
{
  "message": "title and description are required"
}
```

### PUT /todos/{id}
TODOを更新する

パスパラメータ:
| パラメータ名 | 型 | 説明 |
|------------|-----|------|
| id | integer | 更新するTODOのID |

リクエストボディ:
| パラメータ名 | 型 | 説明 |
|------------|-----|------|
| title | string |　更新するタイトル　|
| description | string | 更新するTODOの詳細　|
| done | boolean | 完了状態　|

**リクエスト例**
```json
{
  "title": "買い物",
  "description": "卵を買う",
  "done": true
}
```

**レスポンス(200)**
```json
{
  "id": 1,
  "title": "title",
  "description": "description",
  "done": false
}
```

**レスポンス(404)**
```json
{
  "message": "TODO not found"
}
```

**レスポンス(400)**
```json
{
"message": "invalid request"
}
```

### DELETE /todos/{id}
TODOを削除する

パスパラメータ:
| パラメータ名 | 型 | 説明 |
|------------|-----|------|
| id | integer | 削除するTODOのID |

**レスポンス**
```json
{
  "message": "deleted"
}
```

**レスポンス(404)**
```json
{
  "message": "TODO not found"
}
```