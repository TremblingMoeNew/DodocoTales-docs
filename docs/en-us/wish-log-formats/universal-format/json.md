# Universal Wish Format - JSON Variant

!> This is not a official document.

The JSON Variant of *Universal Wish Format* is designed to achieve a maximum compatibility and retention to the raw data responsed by the Mihoyo API of wish logs, as well as the import and export effciency.

The root object contains two fields: The `info` holds the basic infomation of the wish log file, and the `list` holds all the wish log items.

The file format is roughly as follows:

```json
{
    "info" : {
        "uid" : "000000000",
        "lang" : "en-us",
        ...
    },
    "list" : [
        {
            "gacha_type": "000",
            "time": "yyyy-MM-dd HH:mm:ss",
            "name": "Debate Club",
            "item_type": "Weapon",
            "rank_type": "3",
            "id": "1600099200004770203",
            "uigf_gacha_type": "000",
        },
        ...
    ]
}
```

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

## Basic Info

The `info` field is to store the basic information of the universal wish log files, including the user info, the export info, and other extended info.

### User info

The wish tools need to identify the owner of wish logs via the `uid`, and the `lang` marks the language of **ALL THE** wish log items.

Given that a universal wish log file will contain ONLY ONE USER's wish logs, and the standard stipulates that all the log items should be in a same language, this two fields can be classified as "user info", extracted from the log items, and placeed in the Basic Info section.

According to the UIGF standard, to ensure the information integrity of data exchange, and to the potential need of user privacy protection and information desensitization, the `uid` and `lang` are classified as **RECOMMENDED OPTIONAL FIELDS**.

| Fields   | UIGF Specification  |
| ------ | ----------------------------------------------- |
| `uid`  | OPTIONAL. Recommended to be decided by the users.  |
| `lang` | OPTIONAL. Recommended. ALL THE WISH LOG ITEMS should be in this language. |

### Export Info

The wish log tools need to record some additional information in the universal wish log files, identifying the followed version of UIGF standard, the tool which exported the file, and the export time, ensuring the other tools can correctly handle the file.

The following fields are not the mandatory fields in the UIGF standard, but may be necessary for some tools.

| Field          | Meanings                              | UIGF Specification                                |
| ------------- | ----------------------------------------- | ------------------- |
| `export_time` | File created time | Format should be `yyyy-MM-dd hh:mm:ss` |
| `export_app`  | File created by which application  | Defined by the application |
|`export_app_version`| The application's version |Defined by the application|
|`uigf_versuon`|The version of UIGF Standard the file follows| A [defined](en-us/wish-log-formats/universal-format/uigf-standard.md#uigf_version) UIGF Version|
|`export_timestamp`| The UNIX timestamp of created time | 32-bit UNIX timestamp but as int64. Since UIGF `v2.2`|

### Extended Info

You may add some customized fields in the Basic Info section. This is not a part of the UIGF standard.

Ensure that your customized fields should not be collided with any possibie standard fields that may be added in the future. You may use a special prefix of your own.

## Wish Log Item

The user's wish log items are stored in the `list` array. The items should contain enough necessary infomation, and need to perserve info and structure of the original log item fetched from the Mihoyo's official wish log API in maximum.

### Mandatory Original Info

The UIGF standard specifies some necessary fields. 

All the wish tools should ensure that the log items should contains a vaild following fields：

|    Field     |
| ------------ |
|     `id`     |
|    `name`    |
| `gacha_type` |
| `item_type`  |

#### `id`

The unique number that identifies a wish log item.

Since `id` cannot be got from the official API before version 1.3 of the game, and some wish export tools may not (or once not) save it, the value of this field may have lost.

The standard states that the `id` value of `0-1612303200000000000` should be treated as a Generated Value. When export, the tools should fill the field with a Generated Value if the item is lack of `id`. When import, the wish log item with a Generated `id` should be specially handled to avold the unnecessary confilcts and bugs.

While the UIGF standard states that `id` is a mandatory field, it also require the tools to have the ability to deal with a lacked `id` field.

#### `name`

The name of the item. Should be the official full name of the item.

Should be in `lang` language. 

#### `gacha_type`

The wish type which the item belongs to. Should be the 3-digit numeric code used by the official API.

| `gacha_type` | Official Name |
|-|-|
|`100`|Beginner's Wish<br/>新手祈愿|
|`200`|Permanent Wish<br/>常驻祈愿|
|`301`|Character Event Wish<br/>角色活动祈愿|
|`400`|Character Event Wish-2<br/>角色活动祈愿-2|
|`302`|Weapon Event Wish<br/>武器活动祈愿|

#### `item_type`

The type of the item, i.e. the item belongs to character or weapon.

According to the design idea of UIGF standard - a maximum retention to the raw data - and the value used by Mihoyo API, the value should be `角色` and `武器` in Simplified Chinese, and `Character` and `Weapon` in English.

Should be the same as the value used by Mihoyo API in `lang` language.

### Mandatory Injected Info

The UIGF standard pursues to maintain the original appearance of the wish log items as mush as possible. However, it also introduces some Mandatory Injected Info fields. 

All these injected fields have a `uigf_` perfix.

| Field             | Meanings |
| ----------------- | ---- |
| `uigf_gacha_type` | The class of the pool distinguished by the shared pity count. |

#### `uigf_gacha_type`

Since Version 2.3, the game introduced a new kind of wish pool, the *Character Event Wish-2* (`400`).

This pool has a shared pity count and probability with the *Character Event Wish*. In the official Wish History page, these two pools are joinly displayed as *Character Event Wish and Character Event Wish-2* (`301`).

In order to facilitate the processing of the wish tools, and to ensure the recognition extensibility of the possible addition of other similary wish pool types in the future, the UIGF standard introduces a Mandatory Injected Info field `uigf_gacha_type`.

| `uigf_gacha_type` | Corresponding `gacha_type` | Official Name |
| ----------------- | ---------------- | -------- |
| `100`             | `100` |Beginner's Wish<br/>新手祈愿|
|`200`|`200`|Permanent Wish<br/>常驻祈愿|
|`301`|`301`/`400`|Character Event Wish and Character Event Wish-2<br/>角色活动祈愿与角色活动祈愿-2|
|`302`|`302`|Weapon Event Wish<br/>武器活动祈愿|

### Optional Original Info

The original wish log item contains some other optional info.

| Field | Meanings | Remarks |
| ----- | -------- | ------- |
| `time` | The original time of the item. Without time zone conversion. | **Mandatory field in many implementations**. |
| `rank_type` | Rank of the item. | |
| `count` | No practical effect. | Deprecated field of official API. |
| `item_id` | No practical effect. | Deprecated field of official API. |
| `uid` | User's UID. **Non-Standard Field.** | Should be in `info`. But may exist in log items in some implementations. |
| `lang` | Wish item's language. **Non-Standard Field.** | Should be in `info`. But may exist in log items in some implementations. 