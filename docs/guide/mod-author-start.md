# Mod作成はじめかた

## 必要なもの

- テキストエディタ（VSCode推奨）
- Node.js（zip圧縮に使用）

## ディレクトリ構造

```
MyMod/
├── mod.json
└── main.js
```

## mod.json

```json
{
  "name": "MyMod",
  "version": "1.0.0",
  "author": "あなたの名前",
  "description": "Modの説明",
  "api": "2.0.0",
  "main": "main.js"
}
```

### フィールド一覧

| フィールド | 必須 | 説明 |
|-----------|------|------|
| name | ✅ | 一意な名前（英数字） |
| version | ✅ | セマンティックバージョン |
| author | ✅ | 作者名 |
| description | ❌ | Modの説明 |
| api | ✅ | 対応ForgetAPIバージョン（**v2.0.0 を指定**） |
| main | ✅ | エントリポイントファイル |

!!! warning "v2.0.0 での注意"
    `api` フィールドが `"1.x.x"` の場合、v2.0.0 環境ではロードが拒否されます。必ず `"2.0.0"` に更新してください。

## main.js

```javascript
module.exports = function(ForgetAPI) {
    ForgetAPI.logger.info("MyMod loaded!");
    
    // v2.0.0 新機能の使用例
    ForgetAPI.storage.set("MyMod", "score", 0);
    
    return {
        name: "MyMod",
        version: "1.0.0"
    };
};
```

## .fmファイルの作成

フォルダの中身をzip圧縮して
拡張子を `.fm` に変更。

```powershell
Compress-Archive -Path MyMod\* -DestinationPath MyMod.zip
Rename-Item MyMod.zip MyMod.fm
```

!!! warning "注意"
    フォルダごとではなく中身をzipにしてください。
    解凍後に `mod.json` が直下に来る必要があります。

## テスト

1. `MyMod.fm` を `mods/` に配置
2. ゲーム起動
3. Consoleに以下が出れば成功

```
[INFO] MyMod loaded!
```

## 次のステップ

- [APIリファレンス](../api/core.md)
- [v2.0.0 破壊的変更一覧](../api/core.md#v110-からの破壊的変更)