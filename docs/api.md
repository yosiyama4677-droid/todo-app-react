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

### GET /todos/{id}
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
  "massage":"TODO not found"
}
```

### POST /todos
TODOを作成する

リクエストボディ:
| title | string | 作成したTODOのタイトル |
| description | string | 作成したTODOの詳細　| 

**レスポンス(201)**
```json
{
  "id": 2,
  "title": "title",
  "description": "description",
  "done": false
}
```

### PUT /todos/{id}
TODOを更新する

パスパラメータ:
| id | integer | 更新するTODOのID |

リクエストボディ:
| title | string |　更新するタイトル　|
| description | string | 更新するTODOの詳細　|
| done | boolean | 完了状態　|

**レスポンス(200)**
```json
{
  "id": 1,
  "title": "title",
  "description": "description",
  "done": false
}
```

### DELETE /todos/{id}
TODOを削除する

パスパラメータ:
| id | integer | 削除するTODOのID |

**レスポンス**
```json
{
  "massage": "deleted"
}
```