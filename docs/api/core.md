# API リファレンス (v2.0.0)

ForgetAPI v2.0.0 は、v1.1.0 から大幅に拡張され、**43カテゴリ・約316メソッド・組み込みイベント84種** を提供します。

!!! warning "⚠️ v1.1.0 からの破壊的変更"
    v1.1.0 向けに書かれた Mod は、そのままでは正常に動作しない可能性があります。

    | # | 変更点 | 影響 |
    |---|---|---|
    | 1 | `network.send` がエラー時に **reject** | `try/catch` 必須 |
    | 2 | `file.*` が**サンドボックス化** | ゲームルート外はブロック |
    | 3 | `player.inventory()` が**コピー**を返す | 直接 `.push()` 不可。`addItem` を使用 |
    | 4 | `item.give` が**実際に付与** | 自前付与は二重付与になる |
    | 5 | `world.setFog` が数値を `{density}` に正規化 | `getFog()` の戻り値がオブジェクトに |
    | 6 | Mod ローダーが**メジャーバージョンをチェック** | `api: "1.x.x"` はロード拒否 |

---

## API 使用上の注意

- **永続保存**: `save` は揮発性。永続化には `storage` を使用
- **サンドボックス**: `file.*` はゲームルート外をブロック
- **自動実行**: `statusEffect.tick` / `trigger.check` は本体が自動呼出
- **Input**: Electron レンダラー専用
- **Network**: `fetch` ベース。エラー時は reject

---

## 1. Core

**`getVersion()` / `getInfo()` / `safeRun(callback, modName)` / `registerMod(mod)`**

---

## 2. Logger

**`logger.info(msg)` / `warn(msg)` / `error(msg)` / `getLogs()`**

---

## 3. Event

**`event.on(name, callback)` / `off(name, callback)` / `once(name, callback)` / `emit(name, data)`**

!!! note "主要イベント（v2.0.0 新規含む）"
    `storageSave`, `settingsChange`, `keybindAction`, `statusEffectApply/Remove/Tick`, `triggerEnter/Leave`, `dialogueStart/Node/Choice/End`, `lootRoll`, `extensionRegister/Remove`, `screenActivate/Deactivate/Reset`

---

## 4. Entity

**`entity.add(data)` / `get(id)` / `remove(id)` / `getAll()` / `spawn(id, pos)` / `setModel(id, file)` / `setTexture(id, file)` / `addComponent(id, name, data)` / `registerAI(id, ai)`**

---

## 5. Item

**`item.add(data)` / `get(id)` / `remove(id)` / `give(playerId, id, count)` / `use(id, callback)` / `recipe(data)`**

!!! warning "v2.0.0 変更"
    `item.give` が実際にインベントリへ付与するように

---

## 6. Object

**`object.add(data)` / `get(id)` / `remove(id)` / `replace(id, data)` / `interact(id, callback)`**

---

## 7. Player

**`player.register(id, data)` / `get(id)` / `teleport(id, pos)` / `damage(id, value)` / `heal(id, value)` / `setStatus(id, status, value)`**

**`player.inventory(id)` / `addItem(id, itemId, count)` / `removeItem(id, itemId, count)` / `itemCount(id, itemId)` / `hasItem(id, itemId, count)`** 🆕

!!! warning "注意"
    `damage/heal` はクランプなし。`inventory()` はコピーを返す

---

## 8. Map

**`map.add(data)` / `get(id)` / `remove(id)` / `replace(id, data)` / `load(id)`**

---

## 9. World

**`world.setTime(value)` / `getTime()` / `setWeather(type)` / `getWeather()` / `setFog(data)` / `getFog()` / `addObject(data)`**

!!! warning "v2.0.0 変更"
    `setFog(数値)` は `{density: 数値}` に正規化

---

## 10. Achievement

**`achievement.init(filePath)` / `add(data)` / `unlock(id)` / `has(id)` / `list()`**

---

## 11. Quest

**`quest.add(data)` / `get(id)` / `complete(id, player)` / `reward(id, reward)`**

---

## 12. Horror

**`horror.addJumpscare(data)` / `playJumpscare(id)` / `setFear(value)` / `fog(value)` / `setAtmosphere(data)`**

---

## 13. Story

**`story.addScene(data)` / `play(id)` / `stop()` / `dialogue(character, text)`**

!!! note "分岐会話には v2.0.0 の `dialogue` を使用"

---

## 14. UI

**`ui.addMenu(data)` / `removeMenu(id)` / `showMenu(id)` / `hide(id)` / `notification(message, type)` / `addButton(menu, id, data)` / `setHTML(id, html)` / `appendHTML(id, html)` / `clear(id)` / `addStyle(css)` / `removeStyle(id)` / `setBackground(id, image)` / `setBackgroundColor(id, color)` / `setVideo(id, video)` / `setMusic(id, music)` / `setText(id, text)` / `setImage(id, image)`**

!!! warning "セキュリティ"
    `setHTML` はサニタイズされた HTML のみを渡すこと

---

## 15. Sound

**`sound.add(id, file)` / `get(id)` / `remove(id)` / `play(id, volume)` / `stop(id)`**

---

## 16. Texture / Model / Animation

**`texture.add/replace/remove/get` / `model.add/get/replace/remove` / `animation.add/get/play/stop`**

---

## 17. Shader / PostEffect / Renderer

**`shader.add/apply/disable` / `postEffect.add/enable/disable` / `renderer.setQuality/setResolution/reload`**

---

## 18. Particle / Lighting / Camera

**`particle.add/spawn/remove` / `lighting.add/setAmbient/setFogColor` / `camera.move/shake/rotate/reset`**

---

## 19. Save / Config

**`save.set/get/remove/all/clear` / `config.set/get/has/remove`**

!!! warning "揮発性"
    `save` はメモリのみ。永続化には `storage` を使用

---

## 20. Math

**`math.random(min, max)` / `clamp(value, min, max)` / `lerp(a, b, t)` / `distance(a, b)`**

---

## 21. Timer

**`timer.setTimeout/setInterval/clearTimeout/clearInterval/clear`**

---

## 22. File

**`file.read(path)` / `write(path, data)` / `exists(path)` / `remove(path)`**

!!! warning "v2.0.0 変更"
    サンドボックス化。ゲームルート外はブロック

---

## 23. Input

**`input.isKeyDown(code)` / `isMouseDown(button)` / `mouseX()` / `mouseY()` / `lockMouse()` / `unlockMouse()` / `isLocked()`**

!!! note "Electron レンダラー専用"

---

## 24. Lang

**`lang.add(key, text, lang)` / `get(key, fallback)` / `setLanguage(lang)` / `current()`**

---

## 25. Debug

**`debug.log/warn/error(data)` / `profiler(label)`**

---

## 26. Command

**`command.add(name, callback)` / `remove(name)` / `execute(text)` / `list()`**

---

## 27. Scene

**`scene.add(data)` / `load(id)` / `unload(id)` / `reload()` / `current()`**

---

## 28. Network

**`network.send(url, data, options)` / `receive(channel, callback)` / `disconnect()`**

!!! warning "セキュリティ"
    `try/catch` でエラー処理必須

---

## 29. Registry / Statistics / Scheduler

**`registry.register/get/getAll/remove` / `statistics.set/add/get/reset` / `scheduler.run/repeat/cancel`**

---

## 30. Game / Permission / Dependency

**`game.pause/resume/getState/setState` / `permission.add/has/remove` / `dependency.require/check`**

---

## 31. Resource / Localization

**`resource.texture/sound/model/reload` / `localization.add/get`**

---

## 32. Menu (非推奨)

`ui` のエイリアス。新規コードでは `ui` を使用。

---

# v2.0.0 新規カテゴリ (33〜42)

---

## 33. Storage 🆕

**`storage.set(modId, key, value)` / `get(modId, key, defaultValue)` / `remove(modId, key)` / `keys(modId)` / `clear(modId)`**

!!! note "永続保存"
    `saves/mod_storage/<modId>.json` に保存。イベント: `storageSave`

---

## 34. Settings 🆕

**`settings.define(modId, defs)` / `get(modId, id)` / `set(modId, id, value)` / `getAll(modId)` / `reset(modId)`**

!!! note "スキーマ付き設定"
    `storage` 上に永続化。イベント: `settingsChange`

---

## 35. Keybind 🆕

**`keybind.register(modId, id, defaultCode, label)` / `on(modId, id, callback)` / `off(modId, id, callback)` / `getKey(modId, id)` / `setKey(modId, id, code)` / `list()`**

!!! note "入力アクション抽象化"
    イベント: `keybindAction`

---

## 36. StatusEffect 🆕

**`statusEffect.define(id, def)` / `apply(targetId, effectId, opts)` / `remove(targetId, effectId)` / `has(targetId, effectId)` / `getActive(targetId)` / `clear(targetId)`**

!!! note "時間付きバフ/デバフ"
    `tick(deltaMs)` は本体が自動呼出。イベント: `statusEffectApply/Remove/Tick`

---

## 37. Trigger 🆕

**`trigger.addArea(id, data)` / `removeArea(id)` / `onEnter(id, callback)` / `onLeave(id, callback)` / `isInside(id, entityId)` / `check(entityId, pos)`**

!!! note "領域イベント"
    `check` は本体が自動呼出。イベント: `triggerEnter/Leave`

---

## 38. Inventory 🆕

**`inventory.create(id, options)` / `add(id, itemId, count)` / `removeItem(id, itemId, count)` / `count(id, itemId)` / `has(id, itemId, count)` / `list(id)` / `clear(id)` / `transfer(fromId, toId, itemId, count)`**

!!! note "コンテナ型インベントリ"
    `player.inventory` とは別

---

## 39. Dialogue 🆕

**`dialogue.add(id, tree)` / `play(id, context)` / `choose(index)` / `stop()` / `current()`**

!!! note "分岐会話ツリー"
    イベント: `dialogueStart/Node/Choice/End`

---

## 40. Loot 🆕

**`loot.add(id, entries)` / `get(id)` / `remove(id)` / `roll(id, count)`**

!!! note "ルートテーブル"
    イベント: `lootRoll`

---

## 41. Extension 🆕

**`extension.define(config)` / `call(id, method, ...args)` / `has(id, method)` / `get(id)` / `remove(id)` / `list()`**

!!! note "ユーザーAPI登録"
    コアAPIの上書きは不可。イベント: `extensionRegister/Remove`

---

## 42. Screen 🆕

**`screen.registerSlot(id, options)` / `provide(providerId, config)` / `activate(providerId)` / `deactivate(providerId)` / `active(slot)` / `resetToDefault()` / `layer.add/show/hide/remove` / `theme.set/get`**

!!! note "UI革命"
    1スロット1勝者。`resetToDefault` は脱出ハッチ。イベント: `screenActivate/Deactivate/Reset`