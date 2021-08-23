# github-api

## 串接 Github API 、Infinite Scroll (無限滾動) 、Parallax Scrolling (視差滾動)

- Infinite Scroll 無限滾動：在 mounted 監聽 scroll，當卷軸到一定程度時將資料 push 至渲染資料的 v-for

- Parallax Scrolling 視差滾動：在視差滾動元素上透過 translateY 給予 `(window.pageYOffset * 隨機數) px`，透過使用者滾動頁面的垂直距離來造成視差

## DEMO：https://jimmyanso.github.io/github-api/

## Project setup
```
yarn install
```

### Compiles and hot-reloads for development
```
yarn serve
```

### Compiles and minifies for production
```
yarn build
```

### Customize configuration
See [Configuration Reference](https://cli.vuejs.org/config/).
