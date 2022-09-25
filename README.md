# over-url-loader

> webpack loader; 超出设定大小后 执行自定义操作上传图片至 cdn

### maxSize

文件最大值 , 超出执行 fallback 回调处理

### mappingJson

自定义映射文件路径

### fallback

文件超出大小后执行的回调函数, 返回 promise 对象 ; 可对文件内容进行自定义上传(cdn) 处理

**webpack.config.js**

```js
module: {
  rules: [{
    test: /\.(png|jpg|jpeg|gif)$/,
    type: 'javascript/auto',
    use: [{
        loader: 'over-url-loader',
        options: {
          maxSize: 10 * 1024,
          mappingJson: path.resolve(__dirname, 'img2cdn.json'),
          fallback: (context) => {
            return new Promise((resolve) => {
              setTimeout((context) => {
                resolve('https://webpack.js.org/assets/icon-square-big.svg')
              }, 3 * 1000);
            })
          }
        }
      },
      {
        loader: 'url-loader',
        options: {
          name: '[name].[hash:10].[ext]',
          limit: 8 * 1024,
          esModule: false,
          outputPath: 'img'
        },
      }
    ]
  }]
}
```
