# Uniformed Interchangeable GachaLog Format Standard (UIGF)

!> This is not a official translation.

## Preface

As the wish pools and logs of *Genshin Impact* are getting more complicated, the costs of data exchange between Apps are increasing.

SO WE,

* [biuuu/genshin wish export](https://github.com/biuuu/genshin-wish-export)
* [DGP Studio/Snap.Genshin](https://github.com/DGP-Studio/Snap.Genshin)
* [Scighost/KeqingNiuza](https://github.com/Scighost/KeqingNiuza)
* [sunfkny/genshin gacha export](https://github.com/sunfkny/genshin-gacha-export)
* [TremblingMoeNew/DodocoTales](https://github.com/TremblingMoeNew/DodocoTales)
* [voderl/genshin gacha analyzer](https://github.com/voderl/genshin-gacha-analyzer)

*( Sorted by lexicographic order, which has no any other means. )*

TOGETHER TO DRAW UP THE STANDARD, to enhance the data exchangeability between Apps relevant to the *Genshin Impact* game.

If there is needs to exchange any new forms of data between apps in the future, the new standards would also be made.

## Cautions

> When supporting the format standard, be aware of the underscore `_` and space ` ` character that may exist in the name of some item fields.
>
> This format is available in a **Simplified Chinese** environment only.

### Id

*Genshin Impact*'s wish log item contains a special field `id`. This field was added since the Version 1.3 of the game.

So, **the items logged before that** would not have the corresponding `id` without a special compatibility modification.

When export, 

* Ensure the vaildity of the `id` field of EVERY wish log item,
* It is recommended to set a decreasing `id` value for items with a descending order (by time) starting from the last item with a vaild `id`. The decrease value should be `1`.
* The GENERATED `id` value should be no greater than `1612303200000000000`.
* The Apps should not assume that all the `gacha_item`s have a vaild `id`.
* The Apps should have the ability to handle a null or empty `id` string.

### GachaType

The *Wish* of the game contains kind of pools which have a shared pity count and probability. So, an extra field is needed to make the distinction.

For all the `UIGF` formats, we have injected a `uigf_gacha_type` field into the log items.

Note that, the `uigf_gacha_type` field need to be added when exporting your wish logs to a `UIGF` format file.

#### The Mapping relationships of `uigf_gacha_type`

|`uigf_gacha_type`|`gacha_type`|
|-|-|
|100|100|
|200|200|
|301|301\|400|
|302|302|

## Excel Workbook (Workbook Format)

> Uniformed Interchangeable GachaLog Format Standard of Workbook (UIGF.W)

### Name of the file

We recommend to:

* Contain the `uid` of the user whom the exported data belongs to.
* Give users the right to modify the name of the file before the export process.

### Format of the cells

* When populating the data within a cell, it should be converted to the String type first.

### Name and content of the worksheets

|Name|Content|Type|Necessity|
|-|-|-|-|
|Statistical Analysis|Analyse statistics and more|Any|Optional|
|Character Event Wish<br/>角色活动祈愿|Wish data with a `gacha_type` of `301\|400` |Wish Log Table|Optional, butexpected for export|
|Weapon Event Wish<br/>武器活动祈愿|Wish data with a `gacha_type` of `302`|Wish Log Table|Optional, butexpected for export|
|Permanent Wish<br/>常驻祈愿|Wish data with a `gacha_type` of `200`|Wish Log Table|Optional, butexpected for export|
|Beginner's Wish<br/>新手祈愿|Wish data with a `gacha_type` of `100`|Wish Log Table|Optional, but expected for export|
|Raw Data<br/>原始数据|All the wish log data|Raw Data Table|**See the *Structure of Raw Data Table* section below for detail**|

* The order of the worksheets can be random.
* You can hide parts of the worksheets to prevent the users from tampering with the data.
* The name of the sheets should **match the displayed name of the in-game *Wish History* Page**.

> The data exchange between the Apps should be based on the content of the `原始数据` (`Raw Data`) table.

### Structure of Wish Log Tables

This section is to standardize the compatibility with analytics Apps.

* **The order** of the headers and the corresponding columns **should be arranged strictly as mentioned below**.
* **The pools with a shared pity count** should be distinguished by the type of wish(`gacha_type`).
* This type of sheet is designed to facilitate user's viewing and analysis of the wish log tools.
|Header|Content|Necessity|
|-|-|-|
|Time<br/>时间|Time `time` in `yyyy-MM-dd HH:mm:ss` format|Necessary|
|Name<br/>名称|Name of the item `name`|Necessary|
|Item Type<br/>类别|`item_type`|Necessary|
|Rank<br/>星级|`rank_type`|Necessary|
|Gacha Type<br/>祈愿类型|The map name of `gacha_type`|Necessary, though some tools may not analyse this field|
|...|...|Optional|

> You can add other columns if you think it's necessary. However, please ensure that the first columns should match the specifications above.
>
> The data in the worksheet usually sort in ascending or decending order by *Wish Id*. The analysis Apps should not assume that the order in the table is always in ascend or descend.

#### Map name of `gacha_type`

|gacha_type|Name|
|-|-|
|100|Beginner's Wish<br/>新手祈愿|
|200|Permanent Wish<br/>常驻祈愿|
|301|Character Event Wish<br/>角色活动祈愿|
|400|Character Event Wish-2<br/>角色活动祈愿-2|
|302|Weapon Event Wish<br/>武器活动祈愿|

#### Example

|Time|Name|Item Type|Rank|Gacha Type|...|
|-|-|-|-|-|-|
|2021-02-17 18:45:09|Debate Club|Weapon|3|Character Event Wish-2|...|
|...|...|...|...|...|...|

> (The Simplified Chinese Version)
>
> |时间|名称|类别|星级|祈愿类型|...|
> |-|-|-|-|-|-|
> |2021-02-17 18:45:09|以理服人|武器|3|角色活动祈愿-2|...|
> |...|...|...|...|...|...|

### Structure of Raw Data Table

When export,

* The applications should ask users whether to include the Raw Data Table whenever possible.
* A workbook file would be recognized as UIGF format once it contains a worksheet named `Raw Data` ( `原始数据` ).
* The contents of the table should be filled in strictly as described in this format standard.
* **The order of the headers should be strictly sorted as the sequence in the following table.**
* The existing fields are sorted in **lexicographical ascending order**. The fields that added in the future would be sorted after in introduced time order.
* For no special needs, we recommend to export all fields contained in the json data.
* When importing, it is strongly recommended that you write the programs that do not depend on the order of the columns to achieve the maximum compatibility.
* If you omit the values of some optional fields, leave the header present and the corresponding columns empty.

|Header|Necessity|
|-|-|
|`count`|Optional, but recommend to retain. Not excluding the possibility of a `count` not in "1" value.|
|`gacha_type`|Necessary|
|`id`|Necessary. And most of the Apps sort the data by this field.|
|`item_id`|Optional. This field has been officially deprecated.|
|`item_type`|Necessary.|
|`lang`|Optional, but recommended for internationalization.|
|`name`|Necessary.|
|`rank_type`|Optional, but recommended for analysis.|
|`time`|Optional, but recommended for analysis.|
|`uid`|Optional, but recommended to be decided by the users for analysis.|
|`uigf_gacha_type`|Necessary.|

#### Example

|count|gacha_type|id|item_id|item_type|lang|name|rank_type|time|uid|uigf_gacha_type|
|-|-|-|-|-|-|-|-|-|-|-|
|1|301|1613556360008291100||Weapon|en-us|Debate Club|3|2021-02-17 18:45:09|123456789|301|
|...|...|...|...|...|...|...|...|...|...|...|


> (The Simplified Chinese Version)
>
> |count|gacha_type|id|item_id|item_type|lang|name|rank_type|time|uid|uigf_gacha_type|
> |-|-|-|-|-|-|-|-|-|-|-|
> |1|301|1613556360008291100||武器|zh-cn|以理服人|3|2021-02-17 18:45:09|123456789|301|
> |...|...|...|...|...|...|...|...|...|...|...|

## Json Format

> Uniformed Interchangeable GachaLog Format standard of Json (UIGF.J)

Since the Json format is consistent with the format of the data fetched from official API and is easier for the import and export of the Apps,

here we make the specifications.

This format is only used for the data exchange between apps.

### The export format

With the idea of extracting the same value field to the upper level, we have specified the following json format

```json
{
    "info" : {
        "uid" : "000000000",
        "lang" : "zh-cn",
        ...
    },
    "list" : [
        {
            "gacha_type": "000",
            "item_id": "",
            "count": "1",
            "time": "yyyy-MM-dd HH:mm:ss",
            "name": "以理服人",
            "item_type": "武器",
            "rank_type": "3",
            "id": "1600099200004770203",
            "uigf_gacha_type": "000",
        },
        ...
    ]
}
```

### `info`

In addition to the `uid` and `lang` field extracted from `{gacha_item}`, it can also contain the following fields that we recognize.

|Field Name|Value|Notes|
|-|-|-|
|`export_time`|The time of export: `yyyy-MM-dd HH:mm:ss`||
|`export_timestamp`|The UNIX time stamp of export|v2.2+|
|`export_app`|Name of the app that exported this log file. See the table below for detail.||
|`export_app_version`|Version of the app that exported this log file.||
|`uigf_version`|The `UIGF` version applied by this field. In case a breaking change of `UIGF` occurs, the app cannot handle it.||

#### `uigf_version`

Legal value

|Value|Notes|Compatibility|
|-|-|-|
|`v2.0`|The first official version. |v2.0|
|`v2.1`|Simplify some expressions. Exactly the same as v2.0 in data format.|v2.1 and lower|
|`v2.2`|Add `info.export_timestamp` field filled by the UNIX timestamp. |v2.2 and lower|

#### `export_app`

Use `-` if have no export support.

|Export App|Value of `export_app`|
|-|-|
| [biuuu/genshin wish export](https://github.com/biuuu/genshin-wish-export) | `genshin-wish-export` |
| [DGP Studio/Snap.Genshin](https://github.com/DGP-Studio/Snap.Genshin) | `Snap Genshin` |
| [MUK/应急食品](https://gtool.mukapp.top/)|`MUKGenshinTool`|
| [Scighost/KeqingNiuza](https://github.com/Scighost/KeqingNiuza) | - |
| [Scighost/Xunkong](https://github.com/Scighost/Xunkong) | `Xunkong.Desktop` |
| [sunfkny/genshin gacha export](https://github.com/sunfkny/genshin-gacha-export) | `genshin-gacha-export` |
| [TremblingMoeNew/DodocoTales](https://github.com/TremblingMoeNew/DodocoTales) | - |
| [voderl/genshin gacha analyzer](https://github.com/voderl/genshin-gacha-analyzer) | - |
