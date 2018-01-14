# vue-with-sass
Vue

在Vue-cli脚手架里内引用sass书写css样式，进行如下配置

1.使用save会在package.json中自动添加。

  --1、npm install node-sass --save-dev
  --2、npm install sass-loader --save-dev

注：通常使用npm安装会出现以下报错，安装失败。（网路问题）



 可以通过淘宝的npm镜像安装node-sass，解决以上问题。

$ npm install -g cnpm --registry=https://registry.npm.taobao.org  （安装淘宝镜像）<br/>

$ cnpm install node-sass  --save （使用淘宝镜像安装node-sass）<br/>

注：安装淘宝镜像后，仍无法安装node-sass的情况，执行下列命令
```
$ npm install --save node-sass 

--registry=https://registry.npm.taobao.org 

--disturl=https://npm.taobao.org/dist 

--sass-binary-site=http://npm.taobao.org/mirrors/node-sass
```
说明：
 
--registry=https://registry.npm.taobao.org 淘宝npm包镜像
 
--disturl=https://npm.taobao.org/dist 淘宝node源码镜像，一些二进制包编译时用
 
--sass-binary-site=http://npm.taobao.org/mirrors/node-sass 这个才是node-sass镜像

2、进入webpack.base.config.js 配置scss   module -- loaders (vue1.0)

$ npm install --save-dev sass-loader style-loader css-loader

```{
    test: /\.vue$/,
    loader: 'vue-loader',
    options: {
      loaders: {
        'scss': 'style-loader!css-loader!sass-loader'
      }
    }
  }
```
打开webpack.base.config.js在loaders里面加上  module -- rules (vue2.0)
```
rules: [
      {
        test: /\.vue$/,
        loader: 'vue-loader',
        options: vueLoaderConfig
      },
      {
        test: /\.js$/,
        loader: 'babel-loader',
        include: [resolve('src'), resolve('test')]
      },
      {
        test: /\.(png|jpe?g|gif|svg)(\?.*)?$/,
        loader: 'url-loader',
        query: {
          limit: 10000,
          name: utils.assetsPath('img/[name].[hash:7].[ext]')
        }
      },
      {
        test: /\.scss$/,
        loaders: ["style", "css", "sass"]
      },
      {
        test: /\.(woff2?|eot|ttf|otf)(\?.*)?$/,
        loader: 'url-loader',
        query: {
          limit: 10000,
          name: utils.assetsPath('fonts/[name].[hash:7].[ext]')
        }
      }
    ]
  }
 ```
3、如果需要在vue文件style标签使用scss的话，需要声明一下：

  vue1.0

    ---1、<style rel="stylesheet/scss" lang="scss"></style>

  vue2.0

    ---1、<style lang="scss" scoped="" type="text/css"></style>
