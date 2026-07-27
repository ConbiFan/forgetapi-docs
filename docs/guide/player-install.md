# Mod導入方法

## 対応環境

- Windows 64bit
- 忘却森 v1.0.0以上

## 手順

### 1. Modファイルを入手

`.fm` 拡張子のファイルをダウンロード。

!!! tip "Modの探し方"
    GameJoltで `forget-forest-mod` タグを検索。

### 2. modsフォルダに配置

インストールフォルダ内の `mods/` にコピー。

    忘却森/
    ├── 忘却森.exe
    ├── mods/
    │   ├── mod.txt
    │   └── YourMod.fm
    ├── config/
    └── saves/

### 3. mod.txtを確認

以下になっているか確認。

    enable = true

### 4. ゲーム起動

自動でModが読み込まれます。
タイトル画面の「Mod」ボタンから
有効/無効を切り替え可能。

## トラブルシューティング

| 症状 | 対処 |
| --- | --- |
| Modメニューが出ない | mod.txtをenable=trueに |
| Modがロードされない | .fmを再ダウンロード |
| ゲームがクラッシュ | Mod作者に報告 |
| 実績が消えた | achievements.json確認 |