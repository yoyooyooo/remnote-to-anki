remnote 快速 anki 制卡。

> 相比 quicker 等工具制卡的优势：
>
> 1. 利用 remnote 内置的前端 api，可以获取更多 remnote 内部格式，如不同的高亮颜色。quicker 等工具一般都只能靠复制后处理剪切板，但是 remnote 的一些格式复制不出来，如不同的高亮颜色。
> 2. 制卡不必展开所有子 rem。

## 配置

先安装 [anki-connect](https://ankiweb.net/shared/info/2055492159) 插件，然后设置里加上：

![](https://i.loli.net/2021/05/22/j3exZPbENtGAR4v.png)

然后在 remnote 的插件列表里配置并绑定快捷键：

|             Plugin URL             | CSS Height | CSS width | Permissions | Location |
| :--------------------------------: | :--------: | :-------: | :---------: | :------: |
| https://remnote-to-anki.vercel.app |   100px    |   220px   |    Read     |  Popup   |

其中 Plugin URL 有 3 个参数：

- `modelName`: 卡片类型，默认为 `remnote`
- `deckName`: 牌组，默认为 `test`，当 `deckName=select_manually` 时弹出的窗口可以选择牌组，为其他值时就是指定的牌组名
- `cloze`: 开启挖空模式，详见 [填空题](#填空题)
- `modelName_cloze`，存在 `cloze` 时，[填空题](#填空题)对应的卡片类型，若不存在，则会在正常卡片类型后加`-cloze`后缀，如：正常卡片类型为 `remnote`，填空题卡片类型为 `remnote-cloze`

> 建议添加 2 个插件，分别设置 2 个快捷键，一个为常用牌组，一个为手动选择牌组。

`Plugin URL` 例子：

`https://remnote-to-anki.vercel.app?modelName=remnote&deckName=测试牌组`

> 有条件的建议把 index.html 弄到本地起个服务访问，速度快一点

## 使用

先打开 anki，确保设置了[自定义卡片类型](#参考卡片类型)，或者存在名称为 `remnote` 的卡片类型。然后光标聚焦到某 rem，触发快捷键。**当前聚焦的 rem 为卡片的正面，其所有子 rem 为卡片的背面**。

https://user-images.githubusercontent.com/18062745/119215477-7a3acc80-bb00-11eb-8c9b-ec66fcea096a.mov

## 填空题

默认不处理填空题，当存在参数 `cloze` 时(值可以是任意值，如`cloze=1`)，会把下划线处理成填空题(不用 remnote 默认的`{{...}}`挖空是因为既然选择用 anki 而不用 remnote 自带的 queue，就肯定不希望挖空也同时会被加入 queue)。
同时卡片类型必须包含 `frontside_cloze` 字段，它会被存为挖空后的文本。

> 注意：请确保填空题有对应的卡片类型，规则见[配置](#配置)的 `modelName_cloze`

## 参考卡片类型

### 非填空题

正面：

```
{{frontside}}
```

背面：

```
{{backside}}
```

### 填空题

正面：

```
{{cloze:frontside_cloze}}
```

背面：

```
{{frontside}}
<br>
{{backside}}
```

### 填空题

### 卡片类型 css

```css
.card {
  font-family: arial;
  font-size: 20px;
  text-align: left;
  color: black;
  background-color: white;
}

/* 调整 tab 宽度 */
.rem > .children {
  padding-left: 2em;
}

/* 兼容语法 */
.rem > .main b {
  text-decoration: underline;
}
.rem > .main .quote {
  margin-right: 2px;
  margin-left: 2px;
  background-color: #f0f1f3;
  border-radius: 5px;
  padding: 2px;
}
.rem > .main .block-latex {
  text-align: center;
  margin: 4px 0;
}
.block-latex .mjx-full-width {
  width: unset;
}
.rem > .main,
.rem > .main > * {
  white-space: pre-wrap;
}

/* highlight */
.rem > .main .highlight-red {
  background-color: rgba(255, 0, 0, 22%);
}
.rem > .main .highlight-orange {
  background-color: rgba(244, 167, 98, 0.45);
}
.rem > .main .highlight-yellow {
  background-color: rgba(250, 233, 123, 0.45);
}
.rem > .main .highlight-green {
  background-color: rgba(112, 230, 109, 0.45);
}
.rem > .main .highlight-blue {
  background-color: #ddd;
}
.rem > .main .highlight-purple {
  background-color: rgba(162, 102, 232, 0.45);
}
```
