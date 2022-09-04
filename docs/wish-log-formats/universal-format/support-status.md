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

- 其传统祈愿记录兼容部分表头为`时间`、`名称`、`物品类型`、`星级`、`祈愿类型`、`总抽数`、`距上一个五星`。其`物品类型`列为简体中文取值(`角色`/`武器`)。
- 其`原始数据`表中`count`、`item_id`、`lang`列为空。

其导出的Json格式祈愿记录为通用祈愿格式，适配UIGF`v2.2`标准。

- 其`info`对象具有`uid`、`lang`、`export_time`、`export_timestamp`、`export_app`、`export_app_version`、`uigf_version`七个字段。
- 其`info`对象下的`export_app`字段的取值为`Snap Genshin`。
- 其祈愿项具有`uigf_gacha_type`、`uid`、`gacha_type`、`item_id`、`count`、`time`、`name`、`lang`、`item_type`、`rank_type`、`id`十一个字段。
- 其祈愿项下的`item_id`、`count`、`lang`三个字段取值固定为`null`。

## 刻记牛杂店

!> 该工具已停止维护

该工具具有通用祈愿记录文件导入支持、以及Json格式导出支持。

其支持导入Excel格式与Json格式的通用祈愿格式记录文件。 

其导出的Excel格式祈愿记录为通用祈愿格式，适配UIGF`v2.0`标准。 

- 其传统祈愿记录兼容部分表头为`时间`、`名称`、`物品类型`、`星级`、`祈愿类型`、`总次数`、`保底内`、`祈愿Id`。其`物品类型`列取值视导入时的客户端语言而定。

其不支持Json格式祈愿记录导出。

其导出的通用祈愿格式文件具有以下需要注意的特点或问题：

- 其Excel格式额外具有`统计分析`表、且为工作簿中的第一张表。
- 其祈愿项语言以导出时的游戏客户端语言为准，导出时也并未校验祈愿项语言是否一致。因而，记录文件中可能出现语言非简体中文甚至语言混杂的现象。

## 寻空

该工具具有通用祈愿格式支持。

其支持导入Excel格式与Json格式的通用祈愿格式记录文件。

其导出的Excel格式祈愿记录为通用祈愿格式，适配UIGF`v2.2`标准。 

- 其传统祈愿记录兼容部分表头为`时间`、`名称`、`物品类型`、`星级`、`祈愿类型`、`总次数`、`保底内`、`祈愿Id`。其`物品类型`列取值视导入时的客户端语言而定。

其导出的Json格式祈愿记录为通用祈愿格式，适配UIGF`v2.2`标准。

- 其`info`对象具有`uid`、`lang`、`export_time`、`export_timestamp`、`export_app`、`export_app_version`、`uigf_version`七个字段。
- 其`info`对象下的`export_app`字段的取值为`Xunkong.Desktop`。
- 其祈愿项具有`uid`、`gacha_type`、`item_id`、`count`、`time`、`name`、`lang`、`item_type`、`rank_type`、`id`、`uigf_gacha_type`十一个字段。

其导入通用祈愿格式文件时具有以下需要注意的特点或问题：

- 其并不会从`info`下的`uid`与`lang`字段正确获取记录文件内的祈愿记录项的`uid`和`lang`，而是仅取祈愿记录项中、标准未规定需要包含的`uid`与`lang`字段的值。需要手动在导入页面填写补全。

其导出的通用祈愿格式文件具有以下需要注意的特点或问题：

- 其祈愿项语言以导出时的游戏客户端语言为准，导出时也并未校验祈愿项语言是否一致。因而，记录文件中可能出现语言非简体中文甚至语言混杂的现象。

## 原神抽卡记录导出

该工具不具有祈愿记录导入功能。

其导出的Excel格式祈愿记录为通用祈愿格式，适配UIGF`v2.2`标准。 

- 其传统祈愿记录兼容部分表头为`时间`、`名称`、`类别`、`星级`、`祈愿类型`、`总次数`、`保底内`。其`物品类型`列为简体中文取值(`角色`/`武器`)。

其导出的Json格式祈愿记录为通用祈愿格式，适配UIGF`v2.2`标准。

- 其祈愿项具有`uid`、`gacha_type`、`item_id`、`count`、`time`、`name`、`lang`、`item_type`、`rank_type`、`id`、`uigf_gacha_type`十一个字段。
- 其`info`对象下的`export_app`字段的取值为`genshin-gacha-export`。

## 嘟嘟可故事集

!> 该工具的当前版本(`v0.x`)已基本停止维护且不支持导入与导出功能。以下内容基于开发中的`v1.x`版本。

该工具具有Json格式的通用祈愿格式支持。

其支持导入Json格式的通用祈愿格式记录文件，适配UIGF`v2.1`标准。

其导出的Json格式祈愿记录为通用祈愿格式，适配UIGF`v2.1`标准。

- 其`info`对象具有`uid`、`lang`、`export_time`、`export_app`、`export_app_version`、`uigf_version`六个标准字段及`__ddc_client_region`与`__ddc_timezone`两个自定义扩展字段。
- 其祈愿项具有`gacha_type`、`time`、`name`、`item_type`、`rank_type`、`id`、`uigf_gacha_type`七个字段。
- 其`info`对象下的`export_app`字段的取值为`DodocoTales`。

其导入通用祈愿格式文件时具有以下需要注意的特点或问题：

- 其仅支持其单位数据库中已有的、且名称完全吻合的单位的祈愿记录项导入。

## 应急食品



## NoneBot Plugin GachaLogs

该工具不具有祈愿记录导入功能。

其导出的Excel格式祈愿记录为通用祈愿格式，适配UIGF`v2.2`标准。 

- 其传统祈愿记录兼容部分表头为`时间`、`名称`、`物品类型`、`星级`、`祈愿类型`、`总次数`、`保底内`。

其导出的Json格式祈愿记录为通用祈愿格式，适配UIGF`v2.2`标准。

- 其`info`对象下的`export_app`字段的取值为`nonebot-plugin-gachalogs`。