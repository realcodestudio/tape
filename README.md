
<div align="center">
  <image width="256em" src="https://github.com/user-attachments/assets/276c4a52-8fbe-4fe3-94e7-5f16dab10c1a" />
 </div>
<h1 align="center">Tape 🎞️</h1>


<h3 align="center">Tape 是一个用于实时显示地震信息和气象数据的Web Page，支持简单多源数据轮播展示。</h3>

<h4 align="center">
<a href=https://wolfx.jp>To Wolfx</a> |
<a href=https://x.com/realcodestudio>Follow @RCBS</a> 

## Demo Site

- [tape.bousai.cn](https://tape.bousai.cn)

## 功能特点

- **多模式信息展示**：支持日本气象厅地震信息、中国大陆CENC地震信息、气温排行、降雨排行和自定义内容五种显示模式
- **实时数据更新**：通过API获取最新地震和气象信息
- **动态跑马效果**：底部滚动显示最新信息

## 界面预览

应用界面主要包含以下部分：

- **主要信息**：显示当前模式、最大震度等基本信息
- **底部跑马**：滚动显示最新信息，支持实时更新


## URL参数配置

应用支持通过URL参数自定义行为：

| 参数名 | 可选值 | 说明 |
|--------|--------|------|
| `mode` | `eq`, `cenc`, `temp`, `rain`, `custom` | 设置初始显示模式 |
| `rotate` | `1`, `true`, `yes`, `y`, `on` 或其他值 | 控制是否自动轮播（默认启用） |

示例：
```
http://localhost:11451/tape/index.html?mode=cenc&rotate=false
```

### 显示模式说明

- **eq**：日本地震信息（默认）
- **cenc**：中国地震信息
- **temp**：中国气温排行
- **rain**：中国降雨量排行
- **custom**：自定义内容（可自行修改为直播间规范等）


## 自定义开发

### 修改自定义内容

要修改自定义模式下显示的内容，找到并编辑 `buildCustomText()` 函数：

```javascript
function buildCustomText() {
  return '自定义内容文本...';
}
```

### 调整轮播时间

要修改自动轮播的间隔时间，修改以下代码中的时间值（单位：毫秒）：

```javascript
setInterval(async () => {
  const order = ['eq','cenc','custom','temp','rain'];
  const next = order[(order.indexOf(currentMode) + 1) % order.length];
  await setMode(next);
}, 60 * 1000); // 60秒，可根据需要修改
```

### 调整数据轮询间隔

要修改数据轮询的频率，修改以下代码中的时间值：

```javascript
setInterval(() => { requestLatest(); }, 5 * 1000); // 日本地震数据轮询间隔
setInterval(() => { requestCencLatest(); }, 5 * 1000); // 中国地震数据轮询间隔
```

## 响应式设计调整

系统会根据屏幕大小自动调整字体大小。如需要微调响应式行为，可以修改 `adjustTickerFontSize()` 函数中的相关参数。

## 注意事项

1. 本应用依赖外部API提供数据，如API无法访问或格式变更，可能导致显示异常
2. 由于安全策略限制，在本地文件系统直接打开可能无法正常加载外部数据，建议通过本地Web服务器Python http.server模块应用

## 致谢

特别感谢 [Wolfx Project](https://wolfx.jp) 提供数据。
Icon by [Teenyicons](https://github.com/teenyicons/teenyicons) & [zhangyu1818's AppIcon Forge](https://zhangyu1818.github.io/appicon-forge/).
