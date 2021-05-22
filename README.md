remnote 快速 anki 制卡

## 配置

先安装 [anki-connect](https://ankiweb.net/shared/info/2055492159) 插件，然后设置里加上：

![](https://i.loli.net/2021/05/22/j3exZPbENtGAR4v.png)

然后在 remnote 的插件列表里配置并绑定快捷键：

|             Plugin URL             | CSS Height | CSS width | Permissions | Location |
| :--------------------------------: | :--------: | :-------: | :---------: | :------: |
| https://remnote-to-anki.vercel.app |   100px    |   220px   |    Read     |  Popup   |

其中 Plugin URL 有 2 个参数可以设置，分别是卡片类型 `modelName` (默认 remnote) 和 牌组 `deckName` (默认 test) ，`Plugin URL` 例子：

`https://remnote-to-anki.vercel.app?modelName=remnote&deckName=测试牌组`

## 使用

先打开 anki，然后光标聚焦到某 rem，触发快捷键。

https://user-images.githubusercontent.com/18062745/119215477-7a3acc80-bb00-11eb-8c9b-ec66fcea096a.mov

## 参考卡片类型

必备字段：`正面`, `背面`，

css:

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
