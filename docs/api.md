# APIエンドポイント
実装するエンドポイントを記載する。

## エンドポイント一覧
| メソッド | パス | 説明 |
|--------|------|------|
| GET | /todos/{id} | TODO詳細の取得 |

## エンドポイント詳細

### GET /todo/{id}
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
  "done": false,
}
```
