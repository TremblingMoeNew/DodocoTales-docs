# Universal Wish Format - Workbook Variant

The Workbook Variant of *Universal Wish Format* is designed to achieve a balance between the user-oriented wish log visualizations and the data exchanges.

While achieveing a maximum compatibility and roughly the same visual presentation capabilities with the old *'Classicial Wish Export Format'*, it provides a data import method that is friendly to the wish tools, which can preserve more information and ensures the universality.

So, it can be divided into two sections - the Tranditional Wish Format Compatibility section, and the Raw Data Table section.

In addition, extra costomized worksheets are allowed in the Universal Wish Log files.

## Before Started: The *Classical Wish Export Format*

The term ***Classical Wish Export Format*** in the *Dodocotales Wish Format Library* indicates a family of workbook-based wish log formats with a similar structure as described below.

This format is once widely used. The most famous user is the *Genshin Wish Export* ([biuuu/genshin wish export](https://github.com/biuuu/genshin-wish-export)). It is a previous 'universal' format in some ways.

*Classical Wish Export Format* is not a widely-used name. The name is just for convience.

The Classical Wish Export file contains the following Wish Log Tables:

| TName | Corresponding Official Name   | Corresponding `gacha_type` |
| ------------------ | ---------------------------- | ---------------- |
| Character Event Wish<br/>角色活动祈愿       | Character Event Wish and Character Event Wish-2<br/>角色活动祈愿与角色活动祈愿-2| `301` / `400`    |
|Weapon Event Wish<br/>武器活动祈愿|Weapon Event Wish<br/>武器活动祈愿|`302`|
|Permanent Wish<br/>常驻祈愿|Permanent Wish<br/>常驻祈愿|`200`|
|Beginner's Wish<br/>新手祈愿|Beginner's Wish<br/>新手祈愿|`100`|

In the Wish Log Tables, every row except the first stands for a wish log item, and every column stands for a field.

The Row 1 of the table is the Header, and the wish log items are started from the Row 2 in ascending order.

Column A to F are the following fields:

| Column | Header | Corresponding Field | Format and Notes |
| -- | ------------------ | ---------- | ---- |
|A|time<br/>时间| `time` | `yyyy-MM-dd HH:mm:ss`. The original time of the item. Without time zone conversion. |
|B|name<br/>名称|`name`|Official name|
|C|type<br/>类别|`item_type`|`角色` / `武器` in Simplified Chinese, and `Character` / `Weapon` in English.|
|D|rarity<br/>星级|`rank_type`|Digit, `3`/ `4` / `5`|
|E|total<br/>总次数|——|Equivalent to line number - 1|
|F|within pity<br/>保底内|——|Wish count from the last Rank 5.|

The Column G sometimes may be the `id` field. In this case, the header of Column G is *祈愿Id* *(Wish ID)*

