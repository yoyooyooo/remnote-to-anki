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

