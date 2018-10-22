用sw-precache-webpack-plugin將vue项目升级为pwa项目

1.npm install sw-precache-webpack-plugin  
2.在webpack.prod.config.js中配置：

 ```
const SWPrecacheWebpackPlugin = require('sw-precache-webpack-plugin')  
   new SWPrecacheWebpackPlugin({
    cacheId: 'my-vue-app',
    filename: 'service-worker.js',
    staticFileGlobs: ['dist/**/*.{js,html,css,jpg,png}'],
    minify: true,
    stripPrefix: 'dist/'
})
```
3.在index.html中加入如下代码：  

```
if(navigator.serviceWorker != null){
    navigator.serviceWorker.register('./service-worker.js')
      .then(function(registartion){
        console.log('支持sw:',registartion.scope)
      })
}
```