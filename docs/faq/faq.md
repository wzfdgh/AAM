***
# 目录
* 常见问题
    - pip安装出现问题
    - 群晖NAS使用Python出现奇怪的问题

# 常见问题

## 1) pip安装出现问题
* 如果您直接使用pip进行install遇到
`❗Fatal error in launcher: Unable to create process using pip`
请使用 `python3 -m pip install` 安装

## 2) 群晖 NAS 使用 Python 出现奇怪的问题
* 在群晖NAS中，套件中心安装的 `🐍python3` 环境可能出现奇奇怪怪的问题，请使用第三方套件源
(第三方源需要手动为 `🐍python3` 创建软连接至 `/usr/local/bin/python3` )

## 3) 下载完后出现权限错误
* 如果是您手动创建的目录后出现此问题，请删除目录让脚本自动创建

## 4) Log 保存位置在哪?
* 默认情况下,Log文件会保存在传入的 保存路径 下,当无法访问此路径时,Log保存在工具目录下

## 5) API
> API默认开启,在一般情况下我们不建议关闭
* 当您同时启用 `BGMAPI` 和 `TMDBAPI` 时,如果匹配出的是中文,将会优先使用 `BGMAPI` 识别,如匹配成功再交给 `TMDBAPI` 二次识别,如果没有则让 `TMDBAPI` 识别原匹配

## 6) 什么番剧命名能够被识别?
> 存在番剧剧集,且剧集处于剧名后 (支持的剧集格式为 1-4位纯数字(XXXX集,第XXXX集,第XXXX话,00,XX.XX)/XXEND/XXE//XX END//XX E,若存在 字幕组信息 , 字幕组信息 应在首位
例如:
```
[DMG&LoliHouse] Kono Subarashil Sekai ni Bakuen wo! - 01 [WebRip 1080p HEVC-10bit AAC ASSx2].mkv

[漫游字幕组]散华礼弥/僵尸哪有那么萌 第1集 720P MKV（外挂字幕） [274.7MB].mkv

[织梦字幕组][间谍教室 スパイ教室][11集][1080P][AVC][简日双语] [337.62 MB].mp4
```

> torrent中包含 `[]` `【】` 也可以识别,包含 `04月新番` `（僅限港澳台地區）` `2023.04.02` 之类的字段也可以去除
例如:
```
[Comicat][Jigokuraku][01][1080P][GB&JP][MP4].mp4

[ANi] 無神世界的神明活動（僅限港澳台地區） - 08 [1080P][Bilibili][WEB-DL][AAC AVC][CHT CHS].mp4

[c.c動漫][4月新番][無神世界的神明活動][07][BIG5][1080P][MP4][網盤下載]296.9MB.mkv

[Marukazoku][Sazae-san][2694][2023.04.02][BIG5][1080P][MP4].mp4
```

> torrent中包含 `/` 的将被工具认为是多语种译名番剧,若存在全英文译名将优先采用,不管哪个译名中存在 `S2` `第二季` `Season2` `Season 2` `Season-2` `2nd-Season` 之类的剧季信息也可以识别(如果有需要,后面会开发`シーズン2`之类的剧季识别)
```
【喵萌奶茶屋】★01月新番★[英雄王，为了穷尽武道而转生～然后，成为世界最强的见习骑士♀～ / Eiyuuou, Bu wo Kiwameru Tame Tenseisu][10][720p][简体][招募翻译].mp4

[桜都字幕组] 因为太怕痛就全点防御力了。第2季/ Itai No Wa Iya Nano De Bougyoryoku Ni Kyokufuri Shitai To Omoimasu. S2 [10][ 1080P@60FPS ][简繁内封].mp4
```
> torrent中包含`v2`之类信息的重修版也是可以识别的(在开头的`v2`信息则会被剔除,字幕组信息还是在第一位)
```
[喵萌Production&LoliHouse] 偶像大师 灰姑娘女孩 U149 / THE IDOLM@STER CINDERELLA GIRLS U149 - 07v2 [WebRip 1080p HEVC-10bit AAC][简繁日内封字幕]675.6MB.mkv
```

```
[V2][织梦字幕组][鬼灭之刃 锻刀村篇 鬼灭の刃 刀锻冶の里编][01集][720P][AVC][繁日双语] [614.11 MB].mp4
```
~~> 番剧特别篇,会按TMDB支持的方式进行整理,即特别篇剧季会认定为`Season 00`,剧集则会按TMDB上的来,比如`我推的孩子`的`7.5`集,在TMDB上则是`第1集`~~

## ❓ 什么样的字幕能够被识别?
* 工具目前只支持识别 `简繁日` 字幕，多语种字幕按 `简繁日` 顺序识别一个语种
> 包含 `简` `sc` `chs` `GB` 的会被识别成 `简体字幕`

> 包含 `繁` `tc` `cht` `BIG5` 的会被识别成 `繁体字幕`

> 包含 `日` `jp` 的会被识别成 `日文字幕`