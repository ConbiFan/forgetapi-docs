# Mod作成はじめかた

## 必要なもの

- テキストエディタ（VSCode推奨）
- Node.js（zip圧縮に使用）

## ディレクトリ構造

    MyMod/
    ├── mod.json
    └── main.js

## mod.json

    {
      "name": "MyMod",
      "version": "1.0.0",
      "author": "あなたの名前",
      "description": "Modの説明",
      "api": "1.0.0",
      "main": "main.js"
    }

### フィールド一覧

| フィールド | 必須 | 説明 |
| --- | --- | --- |
| name | ✅ | 一意な名前（英数字） |
| version | ✅ | セマンティックバージョン |
| author | ✅ | 作者名 |
| description | ❌ | Modの説明 |
| api | ✅ | 対応ForgetAPIバージョン |
| main | ✅ | エントリポイントファイル |

## main.js

    module.exports = function(ForgetAPI) {

        ForgetAPI.logger.info("MyMod loaded!");

        return {
            name: "MyMod",
            version: "1.0.0"
        };
    };

## .fmファイルの作成

フォルダの中身をzip圧縮して
拡張子を `.fm` に変更。

    Compress-Archive -Path MyMod\* -DestinationPath MyMod.zip
    Rename-Item MyMod.zip MyMod.fm

!!! warning "注意"
    フォルダごとではなく**中身**をzipにしてください。
    解凍後に `mod.json` が直下に来る必要があります。

## テスト

1. `MyMod.fm` を `mods/` に配置
2. ゲーム起動
3. Consoleに以下が出れば成功

    [INFO] MyMod loaded!

## 次のステップ

- [APIリファレンス](../api/core.md)
- お菓子Modチュートリアル（準備中）