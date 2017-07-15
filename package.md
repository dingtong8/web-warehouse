记录一些平时用过的第三方包，相关 `loader` 设置等，做一下备注整理

----

----

## web

```js

express  // 不用多说了

body-parser  // post

cookies  // cookie

// ---------------------------------------

koa  // koa 核心模块

koa-route  // koa 路由模块

koa-bodyparser  // post

koa-static  // 静态文件加载

koa-static-cache  // 静态文件缓存加载

// ---------------------------------------

co  // 异步（不用编写 Generator 函数的执行器）

co-fs  // 文件流

co-body  // 处理 post

co-views  // 视图模块

// ---------------------------------------

nightmare  // 爬虫用浏览器

nodemailer  // 发送邮件

// ---------------------------------------

cheerio  // node 端的 jquery

underscore  // _

// ---------------------------------------

superagent  // http 方面的库，可以发起 get 或 post 请求

mz  // fs 使用回调，mz 改为 promise

anywhere  // 静态服务器

moment  // 时间操作

supervisor  // 热载

markdown  // 解析 markdown

node-exif  // 读取图片信息

// ---------------------------------------

utility  // md5 之后的值

sha1    // sha1 值

// ---------------------------------------

// 当你需要去多个源(一般是小于 10 个)汇总数据的时候，用 eventproxy 方便（大部分场景）
// 当你需要用到队列，需要控制并发数，或者你喜欢函数式编程思维时，使用 async

eventproxy    // 高等计数器，并行监听多个事件每次当一个源的数据抓取完成时，就通过 ep.emit() 来告诉 ep 自己，某某事件已经完成了

async    // 控制并发连接数

```

## 模版

```js

swig  // 个人用的比较多


nunjucks  // 学习视频时候用了一下

jade  // 功能多

ejs  // 大名鼎鼎

```


## 数据库

```js

mysql  // mysql 驱动

sequelize  // 操作数据库（ORM）

mongoose  // mongodb 驱动

```



## 测试

```js

mocha  // 测试框架

chai  // 断言库

```



## 个人 package.json 配置（基于 vue）

```js

{
    // ...

    "scripts": {
        "dev": "cross-env NODE_ENV=development webpack-dev-server --open --hot --port 3000",
        "build": "cross-env NODE_ENV=production webpack --progress --hide-modules"
    },
    "dependencies": {
        "vue": "^2.2.1",
        "vue-router": "^2.5.3"
    },
    "devDependencies": {
        "babel-core": "^6.0.0",
        "babel-loader": "^6.0.0",
        "babel-preset-latest": "^6.0.0",
        "cross-env": "^3.0.0",
        "css-loader": "^0.25.0",
        "file-loader": "^0.9.0",
        "node-sass": "^4.5.3",
        "sass-loader": "^5.0.1",
        "style-loader": "^0.17.0",
        "vue-loader": "^11.1.4",
        "vue-style-loader": "^3.0.1",
        "vue-template-compiler": "^2.2.1",
        "webpack": "^2.2.0",
        "webpack-dev-server": "^2.2.0"
    }

    // ...
}

```


## 个人 webpack.config.js 配置（基于 vue）

```js

var path = require('path')
var webpack = require('webpack')

module.exports = {
    entry: './src/main.js',
    output: {
        path: path.resolve(__dirname, './dist'),
        publicPath: '/dist/',
        filename: 'build.js'
    },
    module: {
        rules: [
            {
                test: /\.vue$/,
                loader: 'vue-loader',
                options: {
                    loaders: {
                        'scss': 'vue-style-loader!css-loader!sass-loader',
                        'sass': 'vue-style-loader!css-loader!sass-loader?indentedSyntax'
                    }
                }
            },
            {
                test: /\.js$/,
                loader: 'babel-loader',
                exclude: /node_modules/
            },
            {
                test: /\.(png|jpg|gif|svg)$/,
                loader: 'file-loader',
                options: {
                    name: '[name].[ext]?[hash]'
                }
            },
            {
                test: /\.scss$/,
                loaders: ["style", "css", "sass"]
            },
            {
                test: /\.(woff2?|eot|ttf|otf)(\?.*)?$/,
                loader: 'url-loader'
            }
        ]
    },
    resolve: {
        alias: {
            'vue$': 'vue/dist/vue.esm.js'
        }
    },
    devServer: {
        historyApiFallback: true,
        noInfo: true
    },
    performance: {
        hints: false
    },
    devtool: '#eval-source-map'
}

if (process.env.NODE_ENV === 'production') {
    module.exports.devtool = '#source-map'
    module.exports.plugins = (module.exports.plugins || []).concat([
        new webpack.DefinePlugin({
            'process.env': {
                NODE_ENV: '"production"'
            }
        }),
        new webpack.optimize.UglifyJsPlugin({
            sourceMap: true,
            compress: {
                warnings: false
            }
        }),
        new webpack.LoaderOptionsPlugin({
            minimize: true
        })
    ])
}

```
