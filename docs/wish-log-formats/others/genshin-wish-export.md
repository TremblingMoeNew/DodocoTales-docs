# 其他工具 - 原神祈愿导出工具

原神祈愿记录导出工具（Genshin Wish Export）为一款PC端的本地祈愿导出工具。

其为知名度最高、用户量最大的PC端祈愿记录工具，也是具有最多的Star与Fork数量的开源祈愿记录工具。其所使用的祈愿记录导出格式以及部分可视化表示方法于很大程度上已成为事实标准。

其支持多种语言，用户遍布全球，但简体中文下的功能与其他语言下略有差异。

其开源项目地址为[biuuu/genshin-wish-export](https://github.com/biuuu/genshin-wish-export) 。

?> 以下基于原神祈愿导出工具于2022年9月10日时的状态(`v0.8.7`)介绍。

## 导入

原神祈愿导出工具不支持祈愿记录的导入。

开发者提供了从传统祈愿导出格式文件恢复GWE储存格式文件的[工具](https://genshin-gacha-export.danmu9.com/)。

?> 若尝试从通用祈愿格式导入（仅限工作簿格式），您需要确保其中的表按照“角色活动祈愿”、“武器活动祈愿”、“常驻祈愿”、“新手祈愿”、“原始记录”排布。<br/>存在原始记录表时，您的主页上将会增加一张无效的灰色饼图。不必担心，这不影响使用。其将在下一次获取祈愿记录后消失。

## 导出

!> 该工具的祈愿项语言以导出时的游戏客户端语言为准，导出时也并未校验祈愿项语言是否一致，因而可能出现语言混杂的现象。 

原神祈愿导出工具提供了传统祈愿导出格式（XLSX文件）与通用祈愿格式（JSON文件）两种导出方法。

### 传统祈愿导出格式

原神祈愿导出工具默认使用该格式进行导出。

其为一种工作簿格式文件。**表名与表头的命名语言取决于最近一次祈愿记录导出时的游戏客户端语言。**

其具有“新手祈愿”、“常驻祈愿”、“角色活动祈愿”、“武器活动祈愿”四大祈愿类型的祈愿表。

| 表名（简体中文时） | 对应官方名称（简体中文时）   | 对应`gacha_type` |
| ------------------ | ---------------------------- | ---------------- |
| 角色活动祈愿       | 角色活动祈愿与角色活动祈愿-2 | `301` / `400`    |
|武器活动祈愿|武器活动祈愿|`302`|
|常驻祈愿|常驻祈愿|`200`|
|新手祈愿|新手祈愿|`100`|

祈愿表中，除表头外的每一行表示一个祈愿记录项，每一列表示一个祈愿项字段。

祈愿表的行1为表头，行2起为祈愿项。祈愿项按照升序排列。

祈愿表的列A至列G为以下祈愿项字段：

| 列 | 表头（简体中文时） | 对应祈愿项字段 | 格式与备注 |
| -- | ------------------ | ---------- | ---- |
|A| 时间 | `time` | `yyyy-MM-dd HH:mm:ss`。祈愿项原始时间，不进行时区本地转换。 |
|B|名称|`name`|官方名称（简体中文时为中文名）|
|C|类别|`item_type`|官方名称（简体中文时为`角色`或`武器`）|
|D|星级|`rank_type`|数字，`3`/ `4` / `5`|
|E|总次数|——|该祈愿项的序号。相当于行号 - 1|
|F|保底内|——|该祈愿项距离上一五星的抽数|
|G|备注|——||

### 通用祈愿格式

原神祈愿导出工具**在语言为简体中文时**提供“导出JSON”选项，其支持通用祈愿格式。

详情请见[通用祈愿格式 - 支持现状 - 原神祈愿导出工具](wish-log-formats/universal-format/support-status.md#原神祈愿导出工具 "通用祈愿格式 - 支持现状 - 原神祈愿导出工具")。

## 储存格式

原神祈愿导出工具采用基于JSON格式的GWE储存格式保存其祈愿记录信息。

其根对象下包含以下字段：

| 字段      | 含义                               |
| --------- | ---------------------------------- |
| `result`  | 祈愿记录项列表                     |
| `time`    | 最后一次更新时间戳                 |
| `typeMap` | 祈愿类型表                         |
| `uid`     | 祈愿记录所属用户的UID              |
| `lang`    | （最后一次更新时获取的）祈愿项语言 |

文件格式大致如下：

```json
{
    "result" : [
        [
            "301",
            [
                [
                    "yyyy-MM-dd HH:mm:ss",
                    "以理服人",
                    "武器",
                    3
                ],
                [
                    "yyyy-MM-dd HH:mm:ss",
                    "弹弓",
                    "武器",
                    3,
                    "400",
                    "1600099200004770203"
                ],
                ...
            ]
        ],
        [
            "302",
            [...]
        ],
        ...
    ],
    "time" : 1600099200004,
    "typeMap" : [
        [
            "301",
            "角色活动祈愿"
        ],
        ...
    ],
    "uid" : "000000000",
    "lang" : "zh-cn"
}
```



### 祈愿记录项

`result`数组用于存放用户的祈愿记录项。

正常情况下，其中包含四个列表，分别对应角色活动祈愿、武器活动祈愿、常驻祈愿与新手祈愿四种祈愿类型。

对于每个祈愿类型，其第一个对象为祈愿项代号，第二个对象为祈愿项列表。

祈愿项代号如下，其与通用祈愿格式中的`uigf_gacha_type`等价：

| 祈愿项代号 | 对应`gacha_type` | 官方名称（简体中文时） |
| ----------------- | ---------------- | -------- |
| `100`             | `100` | 新手祈愿 |
|`200`|`200`|常驻祈愿|
|`301`|`301`/`400`|角色活动祈愿与角色活动祈愿-2|
|`302`|`302`|武器活动祈愿|

对于祈愿项列表，其包含多个子列表，每个子列表均表示一个祈愿项。祈愿项按升序排序。

祈愿项中的信息按顺序为：

| 对应祈愿项字段 | 含义                                                         |          |
| -------------- | ------------------------------------------------------------ | -------- |
| `time`         | 祈愿项原始时间，不进行时区本地转换。格式为`yyyy-MM-dd HH:mm:ss` | 必要     |
| `name`         | 单位名称。官方名称（简体中文时为中文名）                     | 必要     |
| `item_type`    | 单位类型。官方名称（简体中文时为`角色`或`武器`）             | 必要     |
| `rank_type`    | 单位星级。数字，取值为`3`/ `4` / `5`。                       | 必要     |
| `gacha_type`   | 该次祈愿的细分祈愿类型。 取值为`100` / `200` / `301` / `302` / `400` | 可能缺失 |
| `id`           | 祈愿项ID                                                     | 可能缺失 |

!> 每个祈愿项均为一个列表，祈愿项信息严格按上表顺序排列。<br/>上表中的字段为米哈游官方API返回的祈愿项中的字段，GWE储存格式中的祈愿项**并非键值对储存**。

**其中，后两个属性可能缺失。**

原神祈愿导出工具于2021年11月24日起的V0.7.1版本前并不在祈愿项中保存祈愿类型与ID信息。

从传统祈愿导出格式文件还原的GWE储存格式文件中的祈愿项也同样会丢失该部分信息。

### 其他部分

`time`字段储存用户最后一次更新祈愿记录的UNIX时间戳。

`uid`字段储存该祈愿记录所属用户的UID。

`lang`字段储存该祈愿记录的语言。但由于原神祈愿导出工具在获取记录时采用当前游戏客户端语言，该字段会在每次更新祈愿记录时被刷新，且不能保证所有祈愿项均为该语言。

`typeMap`字段为一个列表，用于储存祈愿项代号所对应的转义名称。其包含四个子列表，每个子列表的第一项为一个祈愿项代号，第二项为该祈愿项代号在当前`lang`下对应的转义名称。`typeMap`在每次更新祈愿记录时被刷新。