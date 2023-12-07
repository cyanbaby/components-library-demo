# components-library-demo
- 本项目由 vue/cli 4.5.19 创建，用来做NPM包转CDN加载的测试。

## 按需导入
```js

// 预先安装
// pnpm install --save-dev babel-plugin-lodash

// 然后配置
// babel.config.js
module.exports = {
  presets: [
    '@vue/cli-plugin-babel/preset'
  ],
  plugins: ['lodash']
}

```