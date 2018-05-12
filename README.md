# LearnWebpack4
Webpack4 新手完全攻略
- 为了优化前端工程, 我们通常会将静态文件压缩,减少带宽占用; 将静态文件合并,减少http请求, webpack可以轻易实现静态文件的压缩合并以及打包的功能, 除此之外, webpack还支持众多的loader插件, 通过loader插件可实现众多类型(如vue, less, jpg, css)资源的打包

-  webpack的文档写的相当出色, 为了方便读者学习, 下面每一类配置的注释里, 都附上了参考的原文档地址, 如果以后配置更新了,也方便查看更新的文档

- 如果不想自己配置, 可以直接拷贝最后的配置文档到自己的项目中, 所有的案例资源附在了文章末尾, 欢迎下载学习

> ![Webpack](https://upload-images.jianshu.io/upload_images/3203841-b0308f5eec5d94da.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


## 新建项目start-webpack, 初始化npm
```shell
mkdir start-webpack
cd start-webpack
npm init -y
```
- 初始化后, npm自动创建npm配置文件

> ![初始化](https://upload-images.jianshu.io/upload_images/3203841-1aa244068d7605cd.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

## 通过npm, 安装webpack
```
npm install -D webpack
# webpack4.0 需要 额外安装webpack-cli
npm install -D webpack-cli
```
- 这里的`-D`表示只在开发阶段使用webpack, 最终打包上线的项目并不需要webpack

> ![安装后](https://upload-images.jianshu.io/upload_images/3203841-a84c74630f7b018b.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

## 手动建立webpack配置文件`webpack.config.js`
> ![webpack.config.js](https://upload-images.jianshu.io/upload_images/3203841-bc37b2779a02846f.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

> ![创建四个文件](https://upload-images.jianshu.io/upload_images/3203841-c387d2eb61247736.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

## 配置`package.json`,自定义webpack打包命令 [官方参考](https://webpack.js.org/guides/getting-started/)
> ![官方参考 https://webpack.js.org/guides/getting-started/](https://upload-images.jianshu.io/upload_images/3203841-ed769bd510b77a3a.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
> ![build](https://upload-images.jianshu.io/upload_images/3203841-9c31d0a8ceb639ad.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

- 运行命令`npm run webpack`, 进行打包, 获得 `./dist/bundle.js`
```
npm run webpack
```
> ![打包文件](https://upload-images.jianshu.io/upload_images/3203841-27d95edd30d9d42b.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
- 测试打包效果
> ![打包成功](https://upload-images.jianshu.io/upload_images/3203841-2bb6291fd131caba.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

## 静态文件打包(以css, 图片为例)
```
# 解决html的输出到dist  参考: https://webpack.js.org/guides/output-management/
npm install -D html-webpack-plugin
# 增加对css的支持 参考: https://webpack.js.org/guides/asset-management/#loading-css
npm install -D style-loader css-loader
# 增加对图片的支持 参考: https://webpack.js.org/guides/asset-management/#loading-images
npm install -D file-loader
```
## 支持less转义打包
```
# 安装 less-loader less 参考:https://webpack.js.org/loaders/less-loader/ 
npm install -D less-loader less
```

## 支持es6语法转义
```
# es6语法转义到es5 参考: https://webpack.js.org/loaders/babel-loader/
npm install "babel-loader@^8.0.0-beta" @babel/core @babel/preset-env
npm install @babel/plugin-transform-runtime --save-dev
npm install @babel/runtime --save
# 使用垫脚片polyfill, 将es6的api实现出来 参考: https://babeljs.io/docs/usage/polyfill/
npm install --save babel-polyfill
```
## 加载使用第三方包 (项目优化方案)
> ![单独加载第三方包](https://upload-images.jianshu.io/upload_images/3203841-ceefebeed813e115.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
```
# 如果将vue打包到bundle.js会增大bundle.js的体积, 所以我们配置使用全局的第三方包, 参考: https://webpack.js.org/configuration/externals/
npm install -S vue
```

## 支持vue.js打包
```
# 支持vue单文件组件加载, 参考:https://vue-loader.vuejs.org/guide/
npm install -D vue-loader vue-template-compiler
```

## 支持自动打包, 支持热重载
> ![保存即生效,无需刷新更新数据](https://upload-images.jianshu.io/upload_images/3203841-12c12977a101c0aa.gif?imageMogr2/auto-orient/strip)



```
# 自动打包工具  参考: https://webpack.js.org/guides/development/
npm install -D webpack-dev-server
# 支持热重载(vue子组件可无刷新更新数据), 参考: https://webpack.js.org/guides/hot-module-replacement/#enabling-hmr
```



> ![发包目录](https://upload-images.jianshu.io/upload_images/3203841-3ddeaea7c39d091e.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
> ![最终项目结构](https://upload-images.jianshu.io/upload_images/3203841-b10edd3db1661f71.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

- 发包命令: `npm install --production`
- 根据`package.json` 下载依赖包 `npm install`
> ![生产环境目录](https://upload-images.jianshu.io/upload_images/3203841-e83ccc616b58731d.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

---
## 最终webpack.config.js配置文件信息: 
```javascript
const path = require('path');
const HtmlWebpackPlugin = require('html-webpack-plugin');
const { VueLoaderPlugin } = require('vue-loader');
const webpack = require('webpack');

module.exports = {

    // 设置垫脚片,设置js入口
    entry: ['babel-polyfill', './src/index.js'],
    // 使用开发服务器, 将服务运行在dist目录中(其实是虚拟于内存中的)
    // 为了解决第三方包的路径问题, 我们将'./dist'改为'./'
    devServer: {
        // 设置虚拟目录所在位置
        // contentBase: './dist'
        contentBase: path.join(__dirname, "./"),
        // 自动压缩输出的文件
        compress: true,
        // 测试端口为 9000
        port: 9000,
        // 热更新组件
        hot: true
    },
    // 解决index.html输出到dist的问题
    plugins: [
        new HtmlWebpackPlugin({
            title: "主页",
            template: "./page.html"
        }),
        new VueLoaderPlugin(),
        new webpack.NamedModulesPlugin(),
        new webpack.HotModuleReplacementPlugin()
    ],
    // 单独 加载使用第三方包
    externals: {
        jquery: 'jQuery',
        vue: 'Vue'
    },
    // 设置 js 输出位置
    output: {
        path: path.resolve(__dirname, 'dist'),
        filename: 'bundle.js'
    },
    module: {
        rules: [
            // 解决加载css资源
            {
                test: /\.css$/,
                use: [
                    'style-loader',
                    'css-loader'
                ]
            },
            // 解决加载图片资源
            {
                test: /\.(png|svg|jpg|gif)$/,
                use: [
                    'file-loader'
                ]
            },
            // 解决加载 less资源
            {
                test: /\.less$/,
                use: [{
                    loader: 'style-loader' // 3. 通过js 以内联样式 插入到页面中
                }, {
                    loader: 'css-loader' // 2. 把css 转化到 js
                }, {
                    loader: 'less-loader' // 1. 把less编译成css
                }]
            },
            // 解决es6转为es5
            {
                test: /\.js$/,
                exclude: /(node_modules|bower_components)/,
                use: {
                    loader: 'babel-loader',
                    options: {
                        presets: ['@babel/preset-env'],
                        plugins: ['@babel/plugin-transform-runtime']
                    }
                }
            },
            // 支持vue的加载
            {
                test: /\.vue$/,
                loader: 'vue-loader'
            }
        ]
    }
};
```

## 最终package.json
```javascript 
{
  "name": "start-webpack",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
    "build": "webpack",
    "start": "webpack-dev-server --open"
  },
  "keywords": [],
  "author": "",
  "license": "ISC",
  "devDependencies": {
    "@babel/core": "^7.0.0-beta.46",
    "@babel/plugin-transform-runtime": "^7.0.0-beta.46",
    "babel-plugin-transform-runtime": "^6.23.0",
    "css-loader": "^0.28.11",
    "file-loader": "^1.1.11",
    "html-webpack-plugin": "^3.2.0",
    "less": "^3.0.2",
    "less-loader": "^4.1.0",
    "style-loader": "^0.21.0",
    "vue-loader": "^15.0.0",
    "vue-template-compiler": "^2.5.16",
    "webpack": "^4.6.0",
    "webpack-cli": "^2.0.15",
    "webpack-dev-server": "^3.1.3"
  },
  "dependencies": {
    "@babel/preset-env": "^7.0.0-beta.46",
    "@babel/runtime": "^7.0.0-beta.46",
    "babel-loader": "^8.0.0-beta.2",
    "babel-polyfill": "^6.26.0",
    "babel-runtime": "^6.26.0",
    "vue": "^2.5.16"
  }
}
```
## 结合以上配置, 用vue组件化的方式写了一个简单的页面
> ![demo](https://upload-images.jianshu.io/upload_images/3203841-82e90b8883f48ab5.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

> 教程涉及到的资源我都通过百度网盘分享给大家,为了便于大家的下载,资源整合到了一张独立的帖子里,链接如下:
http://www.jianshu.com/p/4f28e1ae08b1