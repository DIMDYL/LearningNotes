## taBar

taBar是小程序用于多页面切换的工具

taBar中最少配置两个，最多配置6个

当taBar在顶部的时候是不支持显示icon的只能显示文本信息

#### 配置信息

| 属性            | 类型     | 必填项 | 默认值 | 描述                                |
| --------------- | -------- | ------ | ------ | ----------------------------------- |
| position        | String   | 否     | bottom | tabBar的位置，仅支持bottom/top      |
| borderStyle     | String   | 否     | black  | tabBar上边框颜色，仅支持black/white |
| color           | HexColor | 否     | 无     | tab上文字的默认（未选中）颜色       |
| selectedColor   | HexColor | 否     | 无     | tab上文字的选中颜色                 |
| backgroundColor | HexColor | 否     | 无     | tabBar的背景色                      |
| list            | Array    | 是     | 无     | tab页签的列表(最少2个，最多5个)     |

#### 使用

**在app.json中添加 tabBar ，和window平级**

pagePath：页面路径

iconPath：图标

selectedIconPath：点击图标

text：按钮文字

``` json
  "tabBar": {
      "position": "bottom",
      "borderStyle":"white",
      "color": "#013240",
      "list": [
          {
              "pagePath": "pages/index/index",
              "iconPath": "/imges/QQ截图20240418104411.jpg",
              "selectedIconPath": "/imges/屏幕截图 2024-04-18 104315.png",
              "text": "首页"
          },
          {
            "pagePath": "pages/userindex/userindex",
            "iconPath": "/imges/QQ截图20240418104411.jpg",
            "selectedIconPath": "/imges/屏幕截图 2024-04-18 104315.png",
            "text": "首页"
        }
      ]
  }
```
