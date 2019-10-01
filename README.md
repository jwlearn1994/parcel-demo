# Parcel 使用指南

Parcel 是一款新的打包工具，比起 webpack 4.0 更強化了 0 配置的功能，且其具有強大的快取功能，

能夠更快速的完成基礎打包工作，非常適合作為快速原型開發使用。



## 安裝

基本安裝方式有兩種 global、local

1.  Global 安裝

```cmd
$ npm i -g parcel-bundler
```

2. Local 安裝

```cmd
$ npm i parcel-bundler --dev
```



## 基本使用

首先在專案資料夾內初始化 npm

```cmd
$ npm init -y
```

Parcel 接受任何類型檔案為 entry，建議使用 html 或 js

這邊以 index.html 作為進入點，並使用 vue 來做範例，Parcel 會自動抓取 index.js 作為入口

1. html 模板
```html
<!-- index.html -->
<html>
<body>
  <div id="app"></div>

  <script src="./index.js"></script>
</body>
</html>
```

2. 入口文件
```js
// index.js
import Vue from 'vue'
import App from './App.vue'

new Vue({
  render: h => h(App)
}).$mount('#app')
```

3. Vue App component
```html
<!-- App.vue -->
<template>
  <div id="app" class="container">
    <h3>{{ title }}</h3>
    <p>{{ msg }}</p>
  </div>
</template>

<script>
export default {
  data() {
    return {
      title: 'Hello Parcel Vue',
      msg: 'This is a message'
    }
  }
}
</script>

<style>
#app {
  color: red
}
</style>
```

4. 啟動開發伺服器

輸入下方指令自動在 localhost:1234 建立開發伺服器，內建支援模組熱加載

```cmd
$ parcel index.html
```



## 常用指令

### parcel

預設開啟開發伺服器並監聽變化於 port 1234，並啟用模組熱加載

```cmd
$ parcel index.html
```

### watch

不啟動伺服器，只進行監聽改變，用於已有客製化的伺服器進行服務時。

```cmd
$ parcel watch index.html
```

### build

進行檔案壓縮打包，去除開發模式的偵錯功能，以及模組熱加載，一次性編譯。

```cmd
$ parcel build index.html
```

### --port or -p

可指定開發伺服器的 port

```cmd
$ parcel index.html -p 8080
```

### --public-url

啟動服務的 url，預設為 /。常用於部署打包時，用來調整檔案讀取位置。

```cmd
$ parcel build index.html --public-url ./
```

### --out-dir or -d

修改輸出打包的檔案路徑，預設為 dist。

```cmd
$ parcel build index.html -d build/output
```

### --cache-dir

快取存取路徑，預設為 .cache

```cmd
$ parcel build index.html --cache-dir build/cache
```

### --no-cache

停用快取，預設為啟用快取。

### --https

啟用 https 服務，會產生一個自簽憑證。

```cmd
$ parcel index.html --https
```

### --open

自動於瀏覽器中開啟開發伺服器。

```cmd
$ parcel index.html --open
```

### help

查看 parcel 相關指令說明

```cmd
$ parcel help
```



## 特性功能

### 轉譯器

Parcel 會自動搜尋模組內的設定檔，如.babelrc 和 .postcssrc，並自動執行這些轉換。

### 預設 Babel 轉換

預設 Parcel 使用 @babel/preset-env 進行轉譯，browserlist 預設支援目標為 > 0.25%

### postcss 安裝

預設沒有，需另外加入設定檔如 .postcssrc。

```js
{
  "modules": true,
  "plugins": {
    "autoprefixer": {
      "grid": true
    }
  }
}
```



## 其他

### dist 資料夾清空

parcel 預設不會將 dist 資料夾在每次 build 時清空，可以使用 rimraf 套件進行。

```cmd
$ npm i rimraf
```

```js
// package.json
{
  // ...
  "scripts": {
    clean: "rimraf ./dist && mkdir dist",
    dev: "clean && parcel index.html",
    build: "clean && parcel build index.html --public-url ./"
  }
  // ...
}
```

### Vue 預處理 pug, sass, babel

舉例以使用 Vue 而言，可以直接使用 pug, sass 在 .vue 中，parcel 會在啟用開發模式時，

自動偵測並在需要時進行相關套件的安裝。