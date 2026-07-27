# ForgetAPI Reference

全APIのリファレンス。

---

## Core

### getVersion()

APIバージョンを返す。

    ForgetAPI.getVersion(); // "1.0.0"

### getInfo()

API情報をオブジェクトで返す。

    ForgetAPI.getInfo();
    // {name:"ForgetAPI", version:"1.0.0"}

### safeRun(callback, modName)

エラーを隔離して実行。例外時null返却。

    ForgetAPI.safeRun(() => {
        // 危険な処理
    }, "MyMod");

### registerMod(mod)

Modを登録。通常はローダーが自動呼出。

    ForgetAPI.registerMod({
        name: "MyMod",
        version: "1.0.0",
        instance: modInstance
    });

---

## Logger

### logger.info(msg) / warn(msg) / error(msg)

    ForgetAPI.logger.info("loaded");
    ForgetAPI.logger.warn("deprecated");
    ForgetAPI.logger.error("not found");

### getLogs()

全ログ履歴を配列で返す。

    ForgetAPI.getLogs();
    // [{type, message, time}, ...]

---

## Event

### event.on(name, callback)

    ForgetAPI.event.on(
        "achievementUnlock",
        (data) => console.log(data.id)
    );

### event.emit(name, data)

    ForgetAPI.event.emit("myEvent", {key: "val"});

### event.off(name, callback)

    ForgetAPI.event.off("myEvent", cb);

### 組み込みイベント

| イベント | データ | 説明 |
| --- | --- | --- |
| achievementUnlock | {id} | 実績解除 |
| entitySpawn | {id,pos,health} | 生成 |
| itemGive | {player,item,count} | 付与 |
| mapLoad | {map} | マップ読込 |
| gamePause | - | ポーズ開始 |
| gameResume | - | ポーズ解除 |
| gameRestart | - | 再開 |
| gameQuit | - | 終了 |
| stateChange | {state} | 状態変更 |
| menuOpen | {menu} | メニュー表示 |
| notification | {message,type} | 通知 |
| soundPlay | {id,volume} | 再生 |
| soundStop | {id} | 停止 |
| shaderApply | {shader} | 適用 |
| shaderDisable | - | 無効化 |
| cameraMove | {pos} | カメラ移動 |
| cameraShake | {power,time} | シェイク |
| particleSpawn | {id,pos} | パーティクル |
| ambientChange | {value} | 環境光 |
| fogColorChange | {color} | 霧色 |
| postEffectEnable | {effect} | PE有効 |
| postEffectDisable | {id} | PE無効 |
| jumpscare | {data} | ジャンプスケア |
| fearChange | {value} | 恐怖値 |
| atmosphereChange | {data} | 雰囲気 |
| modRegister | {mod} | Mod登録 |
| modEnable | {mod} | Mod有効 |
| modDisable | {mod} | Mod無効 |
| modReload | {mod} | Modリロード |
| resourceReload | - | リソース再読込 |
| renderQualityChange | {q} | 描画品質 |
| rendererReload | - | レンダラー再読込 |
| weatherChange | {type} | 天候 |
| timeChange | {value} | 時間 |
| questComplete | {quest,player} | クエスト完了 |
| questReward | {id,reward} | 報酬 |
| storyPlay | {scene} | ストーリー再生 |
| storyStop | - | ストーリー停止 |
| dialogue | {char,text} | ダイアログ |
| animationPlay | {id,target} | アニメ再生 |
| animationStop | {id,target} | アニメ停止 |
| playerTeleport | {player} | テレポート |
| recipeAdd | {data} | レシピ追加 |

---

## Entity

### entity.add(data)

    ForgetAPI.entity.add({
        id:"ghost", name:"Ghost", health:100
    });

### entity.get(id) / remove(id) / getAll()

    ForgetAPI.entity.get("ghost");
    ForgetAPI.entity.remove("ghost");
    ForgetAPI.entity.getAll();

### entity.spawn(id, position)

    ForgetAPI.entity.spawn("ghost", {x:10,y:0,z:20});

### entity.setModel(id, file) / setTexture(id, file)

    ForgetAPI.entity.setModel("ghost","g.obj");
    ForgetAPI.entity.setTexture("ghost","g.png");

### entity.addComponent(id, name, data)

    ForgetAPI.entity.addComponent("ghost","ai",{type:"patrol"});

### entity.registerAI(id, ai)

    ForgetAPI.entity.registerAI("ghost", ai);

---

## Item

### item.add(data) / get(id) / remove(id)

    ForgetAPI.item.add({id:"key_red", name:"赤い鍵"});
    ForgetAPI.item.get("key_red");
    ForgetAPI.item.remove("key_red");

### item.give(player, id, count)

    ForgetAPI.item.give("p1","key_red",1);

### item.use(id, callback)

    ForgetAPI.item.use("potion",()=>heal(50));

### item.recipe(data)

    ForgetAPI.item.recipe({output:"sword", input:["iron","stick"]});

---

## Object

### object.add(data) / get(id) / remove(id)

    ForgetAPI.object.add({id:"door",name:"扉"});
    ForgetAPI.object.get("door");
    ForgetAPI.object.remove("door");

### object.replace(id, data)

    ForgetAPI.object.replace("door",{name:"鉄扉"});

### object.interact(id, callback)

    ForgetAPI.object.interact("door", ()=>openDoor());

---

## Player

### player.register(id, data)

    ForgetAPI.player.register("p1",{health:100, position:{x:0,y:0,z:0}});

### player.get(id)

    ForgetAPI.player.get("p1");

### player.teleport(id, pos)

    ForgetAPI.player.teleport("p1", {x:50,y:0,z:50});

### player.damage(id, value) / heal(id, value)

    ForgetAPI.player.damage("p1", 20);
    ForgetAPI.player.heal("p1", 30);

### player.setStatus(id, status, value)

    ForgetAPI.player.setStatus("p1","fear",80);

### player.inventory(id)

    ForgetAPI.player.inventory("p1");

---

## Map

### map.add(data) / get(id) / remove(id)

    ForgetAPI.map.add({id:"forest",name:"森"});
    ForgetAPI.map.get("forest");
    ForgetAPI.map.remove("forest");

### map.replace(id, data) / load(id)

    ForgetAPI.map.replace("forest",{fog:0.06});
    ForgetAPI.map.load("forest");

---

## World

### world.setTime(value) / getTime()

    ForgetAPI.world.setTime(18000);
    ForgetAPI.world.getTime();

### world.setWeather(type) / getWeather()

    ForgetAPI.world.setWeather("rain");
    ForgetAPI.world.getWeather();

### world.setFog(data) / getFog()

    ForgetAPI.world.setFog({density:0.05});
    ForgetAPI.world.getFog();

### world.addObject(data)

    ForgetAPI.world.addObject({type:"tree", pos:{x:10,y:0,z:20}});

---

## Achievement

### achievement.init(filePath)

    ForgetAPI.achievement.init("config/achievements.json");

### achievement.add(data)

    ForgetAPI.achievement.add({id:"first_key", name:"最初の鍵"});

### achievement.unlock(id)

    ForgetAPI.achievement.unlock("first_key");

### achievement.has(id)

    ForgetAPI.achievement.has("first_key"); // true/false

### achievement.list()

    ForgetAPI.achievement.list();

---

## Quest

### quest.add(data) / get(id)

    ForgetAPI.quest.add({id:"q1", name:"鍵を集めろ"});
    ForgetAPI.quest.get("q1");

### quest.complete(id, player) / reward(id, reward)

    ForgetAPI.quest.complete("q1","p1");
    ForgetAPI.quest.reward("q1",{xp:100});

---

## Horror

### horror.addJumpscare(data) / playJumpscare(id)

    ForgetAPI.horror.addJumpscare({id:"scare1", sound:"scream.ogg"});
    ForgetAPI.horror.playJumpscare("scare1");

### horror.setFear(value) / fog(value)

    ForgetAPI.horror.setFear(80);
    ForgetAPI.horror.fog(0.06);

### horror.setAtmosphere(data)

    ForgetAPI.horror.setAtmosphere({fog:0.08, light:0.2});

---

## Story

### story.addScene(data) / play(id) / stop()

    ForgetAPI.story.addScene({id:"intro", text:"森に迷い込んだ..."});
    ForgetAPI.story.play("intro");
    ForgetAPI.story.stop();

### story.dialogue(character, text)

    ForgetAPI.story.dialogue("???", "誰だ...?");

---

## UI

### ui.addMenu(data) / removeMenu(id) / showMenu(id)

    ForgetAPI.ui.addMenu({id:"shop",title:"店"});
    ForgetAPI.ui.showMenu("shop");

### ui.notification(message, type)

    ForgetAPI.ui.notification("保存した","info");

### ui.addButton(menu, id, data)

    ForgetAPI.ui.addButton("shop","buy",{label:"購入"});

---

## Sound

### sound.add(id, file) / get(id) / remove(id)

    ForgetAPI.sound.add("bgm","bgm.ogg");
    ForgetAPI.sound.get("bgm");

### sound.play(id, volume) / stop(id)

    ForgetAPI.sound.play("bgm", 0.8);
    ForgetAPI.sound.stop("bgm");

---

## Texture / Model / Animation

### texture.add / replace / remove / get

    ForgetAPI.texture.add("t1","tex.png");
    ForgetAPI.texture.replace("t1","new.png");

### model.add / get / replace / remove

    ForgetAPI.model.add({id:"m1",file:"m.obj"});

### animation.add / get / play / stop

    ForgetAPI.animation.add({id:"walk"});
    ForgetAPI.animation.play("walk","ghost");
    ForgetAPI.animation.stop("walk","ghost");

---

## Shader / PostEffect / Renderer

### shader.add / apply / disable

    ForgetAPI.shader.add({id:"blur"});
    ForgetAPI.shader.apply("blur");
    ForgetAPI.shader.disable();

### postEffect.add / enable / disable

    ForgetAPI.postEffect.add({id:"vignette"});
    ForgetAPI.postEffect.enable("vignette");

### renderer.setQuality / setResolution / reload

    ForgetAPI.renderer.setQuality("high");
    ForgetAPI.renderer.setResolution(1920,1080);
    ForgetAPI.renderer.reload();

---

## Particle / Lighting / Camera

### particle.add / spawn / remove

    ForgetAPI.particle.add({id:"fire"});
    ForgetAPI.particle.spawn("fire",{x:0,y:0,z:0});

### lighting.add / setAmbient / setFogColor

    ForgetAPI.lighting.add({id:"torch"});
    ForgetAPI.lighting.setAmbient(0.3);
    ForgetAPI.lighting.setFogColor(0x010101);

### camera.move / shake / reset

    ForgetAPI.camera.move({x:0,y:5,z:0});
    ForgetAPI.camera.shake(0.5, 30);
    ForgetAPI.camera.reset();

---

## Save / Config

### save.set / get / remove / all / clear

    ForgetAPI.save.set("score",100);
    ForgetAPI.save.get("score");
    ForgetAPI.save.all();

### config.set / get / has / remove

    ForgetAPI.config.set("diff","hard");
    ForgetAPI.config.get("diff","normal");

---

## Registry / Statistics / Scheduler

### registry.register / get / getAll

    ForgetAPI.registry.register("block","stone",{hardness:3});
    ForgetAPI.registry.get("block","stone");

### statistics.add / get / reset

    ForgetAPI.statistics.add("kills",1);
    ForgetAPI.statistics.get("kills");

### scheduler.run / repeat / cancel

    const id = ForgetAPI.scheduler.run(()=>console.log("done"), 1000);
    ForgetAPI.scheduler.cancel(id);

---

## Game / Permission / Dependency

### game.pause / resume / getState

    ForgetAPI.game.pause();
    ForgetAPI.game.resume();
    ForgetAPI.game.getState(); // "paused"

### permission.add / has / remove

    ForgetAPI.permission.add("admin","conbi");
    ForgetAPI.permission.has("admin","conbi");

### dependency.require / check

    ForgetAPI.dependency.require("DLCAPI");
    ForgetAPI.dependency.check(["DLCAPI"]);

---

## Resource / Localization / Lang

### resource.texture / sound / model / reload

    ForgetAPI.resource.texture("t1","t.png");
    ForgetAPI.resource.reload();

### localization.add / get

    ForgetAPI.localization.add("ja","title","忘却森");
    ForgetAPI.localization.get("ja","title");

### lang.add / get / setLanguage / current

    ForgetAPI.lang.add("title","忘却森");
    ForgetAPI.lang.setLanguage("ja");
    ForgetAPI.lang.current(); // "ja"

---

## Math / File / Network / Timer

### math.random / clamp / lerp / distance

    ForgetAPI.math.random(1,10);
    ForgetAPI.math.clamp(15,0,10); // 10
    ForgetAPI.math.lerp(0,100,0.5); // 50

### file.read / write / exists / remove

    ForgetAPI.file.exists("mods/mod.txt");

### network.send / receive / disconnect

    ForgetAPI.network.send("ch",{msg:"hi"});

### timer.setTimeout / setInterval / clear

    ForgetAPI.timer.setTimeout(()=>{},1000);
