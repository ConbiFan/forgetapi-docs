# Mod導入方法

## 対応環境

- Windows 64bit
- Linux 64bit
- 忘却森 v2.0.0 以上

## 手順

### 1. Modファイルを入手

`.fm` 拡張子のファイルをダウンロード。

!!! tip "Modの探し方"
    GameJoltで `forget-forest-mod` タグを検索。

### 2. modsフォルダに配置

インストールフォルダ内の `mods/` にコピー。

```
ForgetForest/
├── ForgetForest.exe (Windows) / forget-forest (Linux)
├── mods/
│   ├── mod.txt
│   └── YourMod.fm
├── config/
└── saves/
```

### 3. mod.txtを確認

以下になっているか確認。

```
enable = true
```

### 4. ゲーム起動

自動でModが読み込まれます。
タイトル画面の「Mod」ボタンから
有効/無効を切り替え可能。

## セキュリティ

v2.0.0 では以下のセキュリティ機構が導入されています：

- **ファイルサンドボックス**: Modがゲームフォルダ外にアクセスすることはできません
- **ネットワーク通信**: Modが外部通信を行う場合、エラー処理が必須です
- **Zip Slip対策**: 悪意ある `.fm` ファイルによる攻撃を防止

!!! warning "注意"
    Modは自己責任でお使いください。信頼できる作者のModのみを使用することをお勧めします。

## トラブルシューティング

| 症状 | 対処 |
|------|------|
| Modメニューが出ない | `mod.txt` を `enable=true` に |
| Modがロードされない | `.fm` を再ダウンロード |
| ゲームがクラッシュ | Mod作者に報告 |
| 実績が消えた | `achievements.json` 確認 |

## Linux での実行

展開後に実行権限がない場合：

```bash
chmod +x forget-forest
./forget-forest
```