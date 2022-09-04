# 通用祈愿格式 - 支持现状

!> 以下支持列表可能并不完整

当前已知的适配通用祈愿格式的工具如下：

| 祈愿工具         |                     | 平台 | `export_app`            | 导入Excel | 导入Json | 导出Excel | 导出Json |
| ---------------- | ------------------- | ---- | ----------------------- | ------------ | ----------- | ------------ | ----------- |
| 原神祈愿记录导出工具<br/>(Genshin Wish Export) | [biuuu/genshin wish export](https://github.com/biuuu/genshin-wish-export) | PC   | `genshin-wish-export` | :x:          | :x:         | :x:          | `2.1`     |
|Snap.Genshin|[DGP Studio/Snap.Genshin](https://github.com/DGP-Studio/Snap.Genshin)|PC|`Snap Genshin`|`v2.2`|`v2.2`|`v2.2`|`v2.2`|
|刻记牛杂店|[Scighost/KeqingNiuza](https://github.com/Scighost/KeqingNiuza)|PC|:x:|`v2.0`|`v2.0`|`v2.0`|:x:|
|寻空|[Scighost/Xunkong](https://github.com/Scighost/Xunkong)|PC|`Xunkong.Desktop`|`v2.2`|`v2.2`|`v2.2`|`v2.2`|
|原神抽卡记录导出<br/>(Genshin Gacha Export)|[sunfkny/genshin gacha export](https://github.com/sunfkny/genshin-gacha-export)|PC|`genshin-gacha-export`|:x:|:x:|`v2.2`|`v2.2`|
|嘟嘟可故事集(`v1.x`)|[TremblingMoeNew/DodocoTales](https://github.com/TremblingMoeNew/DodocoTales)|PC|`DodocoTales`|:x:|`v2.1`|:x:|`v2.1`|
|应急食品|[MUK/应急食品](https://gtool.mukapp.top/)|Android|`MUKGenshinTool`|||||
|NoneBot Plugin GachaLogs|[monsterxcn/nonebot-plugin-gachalogs](https://github.com/monsterxcn/nonebot-plugin-gachalogs)|NoneBot2|`nonebot-plugin-gachalogs`|:x:|:x:|`v2.2`|`v2.2`|

## 原神祈愿导出工具

该工具不具有祈愿记录导入功能。

其导出的Excel格式祈愿记录并未适配通用祈愿格式，仍为传统祈愿导出格式。	

其导出的Json格式祈愿格式记录为通用祈愿格式，适配UIGF`v2.1`标准。

- 其`info`对象具有`uid`、`lang`、`export_time`、`export_app`、`export_app_version`、`uigf_version`六个字段。
- 其`info`对象下的`export_app`字段的取值为`genshin-wish-export`。
- 其祈愿项具有`gacha_type`、`time`、`name`、`item_type`、`rank_type`、`id`、`uigf_gacha_type`七个字段。

其导出的通用祈愿格式文件具有以下需要注意的特点或问题：

- 该工具具有多语种支持，且祈愿项语言以导出时的游戏客户端语言为准，导出时也并未校验祈愿项语言是否一致。因而，记录文件中可能出现语言非简体中文甚至语言混杂的现象。
- 该工具将`uigf_version`标注为了`2.1`而非标准所规定的`v2.1`。

## Snap.Genshin

该工具具有完整的通用祈愿格式支持。

其支持导入Excel格式与Json格式的通用祈愿格式记录文件，无特殊限制。

其导出的Excel格式祈愿记录为通用祈愿格式，适配UIGF`v2.2`标准。

- 其传统祈愿记录兼容部分表头为`时间`、`名称`、`物品类型`、`星级`、`祈愿类型`、`总抽数`、`距上一个五星`。其`物品类型`列为英文取值(`Character`/`Weapon`)。
- 其`原始数据`表中`count`、`item_id`、`lang`列为空。

其导出的Json格式祈愿记录为通用祈愿格式，适配UIGF`v2.2`标准。

- 其`info`对象具有`uid`、`lang`、`export_time`、`export_timestamp`、`export_app`、`export_app_version`、`uigf_version`七个字段。
- 其`info`对象下的`export_app`字段的取值为`Snap Genshin`。
- 其祈愿项具有`uigf_gacha_type`、`uid`、`gacha_type`、`item_id`、`count`、`time`、`name`、`lang`、`item_type`、`rank_type`、`id`十一个字段。
- 其祈愿项下的`item_id`、`count`、`lang`三个字段取值固定为`null`。

