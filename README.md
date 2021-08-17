# lerna-repo

## 测试文档

## url

[Lerna最佳实践](https://juejin.cn/post/6844903911095025678)
[基于 Lerna 管理 packages 的 Monorepo 项目最佳实践](https://juejin.cn/post/6844903911095025678)

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

上面的配置能用 npm run c 来替换 git commit -m "xx"
选择修改的内容  (下面就是实际效果)
feat: 🎸 添加cz 和commitizen内容

## commitlint && husky

上面无法做到自动触发提交,需要开发自己在commit的时候跑这个指令,可以通过下面来约束

校验工作 用 commitlint, 校验时机 用 husky

```js
// 安装 commitlint 以及要遵守的规范
npm i -D @commitlint/cli @commitlint/config-conventional
// 安装 同时在 package.json 进行配置
npm i -D husky

"husky": {
  "hooks": {
    // 在git 提交时校验提交信息的钩子
    "commit-msg": "commitlint -E HUSKY_GIT_PARAMS"
  }
}
```


## 另外文章备注

[lerna管理前端模块最佳实践](https://juejin.cn/post/6844903568751722509) // 基本知识内容介绍
[基于 Lerna 管理 packages 的 Monorepo 项目最佳实践](https://juejin.cn/post/6844903911095025678)
monorepo(相关package放在一个仓库里管理)和multirepo (每一个package都单独用个仓库管理)
利弊: 前者 多元化发展(有各自的构建工具,依赖管理策略,单元测试), 后者集中管理,减少项目中差异带来的沟通成本

``` js
lerna add chalk                                           // 为所有 package 增加 chalk 模块
lerna add semver --scope @mo-demo/cli-shared-utils        // 为 @mo-demo/cli-shared-utils 增加 semver 模块
lerna add @mo-demo/cli-shared-utils --scope @mo-demo/cli  // 增加内部模块之间的依赖
```

`lerna bootstrap --hoist` // 不同package的依赖提到工程根目录下

或者在lerna.json 里面进行配置 (通过 不用写 --hoist 参数)

```json
{
  "packages": [
    "packages/*"
  ],
  "command": {
    "bootstrap": {
      "hoist": true
    }
  },
  "version": "0.0.1-alpha.0"
}

```

`lerna clean` // 清理所有的依赖
