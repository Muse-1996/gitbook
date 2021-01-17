---
description: 国内可能会有问题，需要科学上网
---

# Electron上手篇

> 目前可能在node v12.2.0版本下有问题，建议切换至v10.16.3

### Electron

> npm init 下载electron

```text
cnpm install electron -g
```

### 脚手架

```text
sudo cnpm install -g electron-forge

electron-forge init myApp
```

#### 创建一个窗口

```javascript
const electron = require('electron')

const { app, BrowserWindow } = require('electron')

let win;

function createWindow () {   
  // 创建浏览器窗口
  win = new BrowserWindow({ width: 420, height: 680, frame:false})

  // 然后加载应用的 index.html。
  win.loadFile('./view/index.html')

  win.on('closed', () => {
      win = null
    })
}



app.on('ready', createWindow)
```

> frame:false 表示无边框窗口

