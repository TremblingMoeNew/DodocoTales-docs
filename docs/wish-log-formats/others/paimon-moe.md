# Paimon.moe

!> 该工具可能难以在中国大陆地区正常访问

[Paimon.moe](https://paimon.moe)为一款网页版的原神助手，其具有材料规划辅助、游戏进度记录和祈愿记录导出功能。

其主要用户为国际服玩家，语言为英文。其界面提供了本地化翻译。

其开源项目地址为[MadeBaruna/paimon-moe](https://github.com/MadeBaruna/paimon-moe) 

?> 以下基于Paimon.moe于2022年9月10日时的状态介绍。

## 导入

该工具支持“Paimon.moe Export”、“Biuuu Gacha Export”、“GeshinWishes Export”与“WishTally”四种Excel导入选项。

其中，“Paimon.moe Export”支持Paimoe.moe祈愿导出格式，“Biuuu Gacha Export”支持传统祈愿导出格式。

> “Biuuu Gacha”即为“原神祈愿导出工具”（[biuuu/genshin wish export](https://github.com/biuuu/genshin-wish-export)）

!> Paimoe.moe仅支持从英文的祈愿导出文件进行导入，这使其无法与现有的通用祈愿工作簿格式文件的实现兼容，也无法使用非英文游戏客户端下由“原神祈愿导出工具”记录并导出的祈愿记录。

## 导出

该工具采用自定义的Paimoe.moe祈愿导出格式。其为一种基于工作簿的格式，且**固定采用英文**。

其设计侧重于取得面向用户的记录可视化展示。

### 表名

其包含“新手祈愿”、“常驻祈愿”、“角色活动祈愿”、“武器活动祈愿”四大祈愿类型的祈愿表，一个“卡池列表”表以及一个元信息表。

表名及顺序如下：

| 表名 | 对应官方名称（简体中文时） | 对应`gacha_type` | 类型 |
| ---- | -------------------------- | ---------------- | ---- |
| Character Event | 角色活动祈愿与角色活动祈愿-2 | `301` / `400`| 祈愿表          |
|Weapon Event|武器活动祈愿|`302`|祈愿表|
|Standard|常驻祈愿|`200`|祈愿表|
|Beginners' Wish|新手祈愿|`100`|祈愿表|
|Banner List|——|——|卡池列表|
|Information|——|——|导出文件元信息|

### 祈愿表结构

祈愿表中，除表头外的每一行表示一个祈愿记录项，每一列表示一个祈愿项字段。 

祈愿表的行1为表头，行2起为祈愿项。 祈愿项按升序排列。

祈愿表的列A至列H按顺序为以下祈愿项字段：

| 列   | 表头 | 意义 |
| ---- | ---- | ---- |
| A    | Type | 单位类型，取值为`Character` / `Weapon` |
| B    | Name | 单位名称，为官方英文名称 |
| C    | Time | 祈愿时间，格式为 `yyyy-MM-dd hh:mm:ss` |
| D    | ⭐   | 单位星级 |
| E    | Pity | 单位抽取所用抽数统计（小保底，不同星级分别统计） |
| F    | #Roll | 当前卡池下抽数统计 |
| G    | Group | 同一个单抽或十连视为一组 |
| H    | Banner | 卡池名，为官方英文名称 |

?> 若需要进行格式转换，您可以借助Paimon.moe的[简中本地化文件](https://github.com/MadeBaruna/paimon-moe/blob/main/src/locales/items/zh.json)（[CDN地址](https://cdn.jsdelivr.net/gh/MadeBaruna/paimon-moe@main/src/locales/items/zh.json)）或其他工具的单位数据库进行单位名称的映射。

### 其他表结构

!> 对于其他祈愿记录工具可能无实际作用

“Banner List”表中：

- 除表头外的每一行表示一个卡池项，每一列表示一个卡池项字段。
- 列A至列C按顺序为以下字段： 


| 列   | 表头 | 意义                  	|
| ---- | ---- | --------------------|
| A    | Name | 卡池名，为官方英文名称     |
| B | Start | 卡池开始时间 |
| C | End | 卡池结束时间 |

“Information”表中：

- A1-B1单元格合并，内容为“Paimon.moe Wish History Export”。
- A2单元格为“Version”。B2单元格为该文件的Paimoe.moe祈愿导出格式版本号，当前为`3`。
- A3单元格为“Export Date”。B3单元格为该文件的导出时间，格式为`yyyy-MM-dd hh:mm:ss` 。

## 储存格式

!> 仅介绍其中部分可用于祈愿记录导出的结构，请勿尝试通过生成该文件进行直接导入。

Paimon.moe采用基于JSON格式的Paimon.moe用户信息文件储存其用户信息。

其根对象下的以下字段可用于祈愿记录导出：

| 字段名                         | 意义                |
| ------------------------------ | ------------------- |
| `wish-uid`                     | 祈愿记录所属用户UID |
| `wish-counter-character-event` | 角色活动祈愿对象    |
| `wish-counter-weapon-event`    | 武器活动祈愿对象    |
| `wish-counter-standard`        | 常驻祈愿对象        |
| `wish-counter-beginners`       | 新手祈愿对象        |

其中，四个`wish-counter`对象下均具有`pulls`字段，其为一个数组，升序储存用户的对应类型祈愿项。

祈愿项至少具有以下字段：

| 字段名 | 意义                                                         |
| ------ | ------------------------------------------------------------ |
| `type` | 单位类型，取值为`character`或`weapon`                        |
| `code` | 单位的`gacha_type`                                           |
| `id`   | 单位的**Paimon.moe ID**，由官方英文名改写而成。**并非官方的祈愿记录项ID**。 |
| `time` | 祈愿时间，格式为 `yyyy-MM-dd hh:mm:ss`                       |

?> 您可以从Paimon-moe项目的代码中获取**Paimon.moe ID**与[角色](https://github.com/MadeBaruna/paimon-moe/blob/main/src/data/characters.js)（[CDN](https://cdn.jsdelivr.net/gh/MadeBaruna/paimon-moe@main/src/data/characters.js)）及[武器](https://github.com/MadeBaruna/paimon-moe/blob/main/src/data/weaponList.js)（[CDN](https://cdn.jsdelivr.net/gh/MadeBaruna/paimon-moe@main/src/data/weaponList.js)）的官方英文名称的对应关系，再借助Paimon.moe的[简中本地化文件](https://github.com/MadeBaruna/paimon-moe/blob/main/src/locales/items/zh.json)（[CDN](https://cdn.jsdelivr.net/gh/MadeBaruna/paimon-moe@main/src/locales/items/zh.json)）或其他工具的单位数据库进行单位名称的语言映射。
