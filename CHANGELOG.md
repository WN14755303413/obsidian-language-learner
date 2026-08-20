# Changelog

> This file is auto-generated from GitHub Releases. Do not edit by hand.

## 0.2.8 - 2026-07-15

+ 升级依赖项
+ 修复移动端白屏问题
+ 删除已失效的句酷词典和pdf功能

## 0.2.7 - 2024-12-16

### Fix
+ 修复spaced repetition界面无法播放单词发音的问题
+ 修复阅读界面音频无法播放的问题

### Tip
目前阅读界面音频支持三种格式：
+ 音频网址，如：`langr-audio: https://upload.wikimedia.org/wikipedia/commons/5/50/Jfk_rice_university_we_choose_to_go_to_the_moon.ogg`
+ 相对库路径，如：`langr-audio: ~/LingQ/河野マリナ - Weight of the World／壊レタ世界ノ歌.mp3`
+ 系统绝对路径，如：`langr-audio: D:/utDownload/岡部啓一 - イニシエノウタ／贖罪.mp3`

## 0.2.6 - 2024-10-20

+ 修复了无法添加本地音频的问题
+ 修复了obsidian 1.7 版本后，插件报错导致软件无法打开的问题

## 0.2.5 - 2023-01-06

+ 增加 deepl 翻译
+ 支持修改复习数据库中的分隔符(设置页面中) #75 
+ 增加查词时是否自动发音的选项 #69 
+ 弹出式查词面板可以通过 `esc` 关闭，配合查词命令，可以手不脱离键盘进行阅读

---

+ 调整新词面板中笔记和例句添加按钮的排列方向和大小
+ 查词面板中各词典增加图标 #76 

---

![image](https://user-images.githubusercontent.com/13451866/211045859-b3d729fb-241b-4c6b-9e1e-d949f95f38eb.png)

![image](https://user-images.githubusercontent.com/13451866/211046741-985ef232-2ad1-416e-8b15-fc218f9738aa.png)

![image](https://user-images.githubusercontent.com/13451866/211046854-0c75544c-d127-40d7-9a6e-f32b5d8fe910.png)

## 0.2.4 - 2022-12-07

+ 修复无法关闭弹出式查词面板的问题 #66 
+ 优化弹出式查词面板弹出的位置
+ 适配手机版obsidian #20 （目前仅测试了安卓平台）

<img src="https://user-images.githubusercontent.com/13451866/206339565-fa2402ea-287b-49b1-a0d2-950be1bee3c9.png" width="170">     <img src="https://user-images.githubusercontent.com/13451866/206339579-3a97d982-3c01-4af5-a8cd-129717519567.png" width="170">     <img src="https://user-images.githubusercontent.com/13451866/206339585-3982d6c9-7c7d-43b7-9821-9d8ecc6cb2dc.png" width="170">     <img src="https://user-images.githubusercontent.com/13451866/206339593-2327cfbc-799f-475e-8dfe-4815e7aafd28.png" width="170">

### 注意
+ 移动端阅读模式选词方法为双击单词，选词组方法为依次点击起始和终止的两个单词
+ 移动端PDF中选词方法为先选中单词文本，然后再点击其他地方取消选中，此时会打开查词面板
+ 若需要在pdf中查词，需要替换新的pdf文件夹（方法见`0.2.0`版release说明）
+ **数据不存在库中，因此单词数据并不会随库文件同步而同步**

## 0.2.3 - 2022-12-05

+ 增加弹出式查词面板 #49 

![image](https://user-images.githubusercontent.com/13451866/205667286-bd934927-60bc-4c00-ac8b-f4663128ac77.png)

## 0.2.2 - 2022-12-04

+ 增加`单词列表`面板，限制可以按照学习状态、tag、搜索对单词数据进行查看
+ 增加阅读模式下记笔记时，同步查看markdown渲染结果的区域。
+ 调整查词面板和新词面板的样式，按钮和输入框变小一些
+ 支持langr-audio中以`~`代表库路径。 如`langr-audio: ~/Mp3/audio.mp3` #44 

![image](https://user-images.githubusercontent.com/13451866/205486670-313cb78a-4578-4bdd-8825-b29b047d3175.png)

![image](https://user-images.githubusercontent.com/13451866/205486860-07e10e85-da86-43bc-aebb-786b9b546e10.png)

+ 修复初次安装文件夹中没有`data.json`而导致读取配置失败，插件无法打开的问题 #53 
+ 修复设置面板中某些开关设置后，重启后被重置的问题 #55 
+ 修复某些例句获取机器翻译失败时，单词无法提交到新词面板的问题 #52

## 0.2.1 - 2022-11-24

+ 增加繁体中文界面支持 感谢 @emisjerry   42e5c23
+ 修复阅读模式行高设置无效的问题
+ 优化查词`seaching...`字样的显示逻辑

从`0.1.x`更新的用户请先阅读一下`0.2.0`版的release说明

**若出现在新库无法打开插件的情况，见#53**，下一版中修复

## 0.2.0 - 2022-11-23

### 功能
+ 支持多词典同时查词 #41 
+ 添加新词典，更多语言：
    + 剑桥词典(中英) #6 
    + 句酷(中英)
    + 沪江小D(中-英法德西日韩) #19 
+ 添加导出学习单词(仅单词)的设置选项 #46 
+ 添加服务器功能，与chrome插件交互
+ 简化查词逻辑，现在可以使用按住功能键同时，鼠标划词或双击来搜索单词
+ 支持调整阅读模式下文字的大小和字体（在设置面板中） #38  #24 
+ 添加了阅读模式下的单词分类计数条 #46 

![image](https://user-images.githubusercontent.com/13451866/203503446-45cd0c04-eb4f-4f4e-bf0a-808ca4b3b7d6.png)
![image](https://user-images.githubusercontent.com/13451866/203503897-40c78c9c-b099-42cc-88c0-4a177d406366.png)
![image](https://user-images.githubusercontent.com/13451866/203503896-20b2e7f5-7a53-4f29-9e52-b0519d33d6bc.png)

### 调整和修复
+ 调整了新词面板的一些样式
+ 解决了切换敏感陌生时样式不跟随变化的问题
+ 阅读模式下单击单词会直接打开查词面板，不再需手动打开
+ 修正了未设置文本数据库导致提交单词时报错的问题

### 特殊

+ 支持PDF查词*
>ob自带的PDF阅读器中无法捕捉点击事件，因此需要使用经过修改的阅读器，将附件中的`pdf.zip`压缩包解压至插件目录下，保证`.obsidian/plugins/obsidian-language-learner/pdf/web/viewer.html`这条路径是通畅的，然后重启obsidian，即可替换自带的阅读器

## 0.1.1 - 2022-10-30

+ 阅读模式会过滤文中的中文字符 #27 
+ 复习数据库不再使用增量更新，而是会读取已有单词的复习数据，合并更新。 因此不会再出现同一个词被添加多遍的情况。#33 #32 #26 
+ words字段启用。 #31 
    + 当在文本中放入`^^^words`，每次退出阅读模式时，会将该篇文章中所有**非无视单词**及其释义更新在该字段下。 
    + 如果文中无`^^^words`字段，不会自动添加，默认为不使用此功能。
    + `^^^words`放置的位置不限

## 0.1.0 - 2022-10-22

### 重要功能
+ 支持分页阅读，阅读长篇文章、小说更方便。 支持记录最后阅读位置。
+ 支持记笔记(notes模块)
+ 测试文件已上传至[文档仓库](https://github.com/guopenghui/language-learner-texts)

新界面：
<img src="https://user-images.githubusercontent.com/13451866/197324221-0b8a638f-01d2-439d-a4ef-d5c4f38dba4d.png" width=330px> <img src="https://user-images.githubusercontent.com/13451866/197324247-157bc344-a2b2-429d-be38-ac654aeee171.png" width=330px >

### 功能改进
+ 可设置自动翻译例句填充新词面板
+ 自动判断单词和词组，填充【种类】选项 #22 
+ 已记录过的词可在新语境下补充例句（自动填充）
+ `article`、`notes`和`words`三个部分不再要求顺序，可以自由安排位置 #30 
+ 修改文章默认字体为Times New Roman，可在`styles.css`文件中自行修改
+ 单词数据库支持自定义分隔符(逗号、tab和 | )，注意与`various complements`中的设置保持一致 #29  
+ 可设置在新词面板提交单词时自动刷新两个文本数据库（单词、复习）  #17 

### 修复
+ 修改了部分图标以区别系统图标
+ 修改了部分颜色样式以适应obsidian`1.0.0`更新

## 0.0.5 - 2022-09-22

+ 设置中增加了【导出“无视”单词】的功能，方便在不同库之间相互补充需要无视的单词
+ 添加了切换阅读模式和markdown模式的快捷键
![image](https://user-images.githubusercontent.com/13451866/191789023-135d655c-b97d-4094-9251-dfb9b9ee35bb.png)
![image](https://user-images.githubusercontent.com/13451866/191789254-52e521d9-ff92-4337-91b0-f61c879e3c9b.png)
+ 添加【含义】时支持多行文本框：
![image](https://user-images.githubusercontent.com/13451866/191789799-168935e7-af5a-481f-94db-cb91e5b6f526.png)
+ 复习单词卡片现在支持发音，点击单词即可

+ 修复了刷新单词数据库时，【反向查询】部分会包含“无视单词”的问题

## 0.0.4 - 2022-06-11

+ 修复了添加多个例句时无法提交的问题
+ 阅读视图下，选中词组只需左键划词一步即可
+ 增加整句机器翻译功能（当选中的单词较多时会自动从查词切换到翻译）
+ 删除有道词典的`权威例句`模块，添加`词组`和`同根词`模块
+ 词典内链接支持内部跳转（即不会打开外部浏览器窗口，而是直接查新词）
+ 词典输入框支持回车确定
+ 词典支持`前进`和`后退`显示历史查询

![xxx](https://user-images.githubusercontent.com/13451866/173178620-b4770df4-f05c-4800-ac37-4bd705c28b75.gif)

## 0.0.3 - 2022-06-01

+ 支持了多数据库（每个笔记库可以有单独的数据库）
+ 支持数据导入和导出

说明：
由于IndexDB是**整个obsidian只有一份**，所以之前无论在哪个库中打开插件，使用的都是同一个数据库(WordDB)

但是很显然会有不同库使用不同数据库的需求，因此此次更新支持了更换数据库，以及导入导出数据的方法。

查看数据库：
按`Shift+Ctrl + I` (大写i)打开开发者工具，在应用(Application)中找到IndexDB，在其中就可找到WordDB（默认的初始库名字）
![image](https://user-images.githubusercontent.com/13451866/171462226-f309e460-f76a-4036-b196-7bd3253ecd79.png)

更名数据库：
1. 先在设置中将原有的数据库导出（得到一个json文件）
2. 在设置中修改数据库的名字
3. 重启软件 (如果新数据库本不存在，则会自动创建)
4. 在设置中导入原有数据：选择之前导出的json文件，点击确定，即完成导入。
5. 可以在开发者工具中手动删除原来的数据库

切换数据库：
1. 修改数据库名字
2. 重启软件

![image](https://user-images.githubusercontent.com/13451866/171464152-fe229b12-150c-482a-a510-77e91cc462bc.png)

## 0.0.2 - 2022-05-29

修复点击"完成阅读"按钮报错的问题，现在可以正常批量添加无视单词

![xxx](https://user-images.githubusercontent.com/13451866/170875192-ae39fd7c-ed3c-4190-859f-986a9b68c254.gif)

## 0.0.1 - 2022-05-27

都在readme里面了

---

_Generated from releases in `guopenghui/obsidian-language-learner`._
