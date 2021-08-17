# lerna-repo

## 测试文档

## url

[Lerna最佳实践](https://juejin.cn/post/6844903911095025678)


## 优雅的提交

安装相关的库

```js
npm i -D commitizen
npm i -D cz-lerna-changelog
```

配置 package.json 去配置config

```json
"scripts": {
    "c": "git-cz"
  },
  "config": {
    "commitizen": {
      "path": "./node_modules/cz-lerna-changelog"
    }
}

```
