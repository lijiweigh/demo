# 到家平台vue项目模板
基于http://git.daojia-inc.com/fe-jz/vue-common 修改。


## Usage


```` bash
$ npm install -g vue-cli

$ vue-init -c gitlab:git.daojia-inc.com:felib/pt-vue-common  [项目目录名]

# 或也可以先把模版clone到本地，然后
$ vue init [模版文件的本地路径] [项目目录名]

$ cd [项目目录名]

# install dependencies
$ npm install

# serve with hot reload at localhost:8080
npm run dev

# 测试环境构建（如果build后不加参数默认为test）
npm run build:test

# 沙箱环境构建
npm run build:sandbox

# 线上环境构建
npm run build:prod

````

## 配置mock数据
在mock目录，添加一个目录用以区分不同的空间，然后在目录里添加一个mock数据文件，可以参考mock/pa/a.js；
如果项目比较小，也可以不同区分不同的空间，直接在mock下新建一个mock数据文件，参考mock/test.js
开发过程，mock文件修改时，自动会加载页面；

## 合并雪碧图配置
有两种方式
### 方法1：对于小型项目，整个项目所有的图标都合并到一张图上
1. 把`config/index.js` 中

`useSprite`设置为true
`src`中的`path`属性设置需要合并的小图标文件的路径，缺省是`src/assets/sprite/icons/`
`target`属性配置 合成的css/scss/图片的文件路径

2. 在使用图标的样式中，`@import url(../style/sprite/sprite.css);`，在dom中直接引用合成后的图标样式'ico-xxx'，可以参考src/page/foo.vue

### 方法2：大型项目，一个页面的图标合到一张图片上，
1. 把`config/index.js` 中`userMySprite`设置为true
2. 每一个页面的图标文件单独存放在`src/assets/sprite/`的一个独立的文件夹中，例如`src/assets/sprite/icon/`
3. 在css文件中引用到背景图片url添加`\?_sprite`后缀例如：

````
background-image: url("../assets/sprite/icon/present.png?_sprite");
````

4、构建后，每一个页面的css中图片自动合成到一张图片上，同时修改相关的样式属性


## 开发过程，要代理某个api到特定的url上，例如线上或测试环境
在.api-proxy.js中增加或修改需要代理的api的地址即可，修改后需要重启服务

## 路由的写法参考`src/router/index.js`
支持动态加载某个页面的资源和直接打包到一个js文件中

## vuex使用提供两种示例，参考`src/store/`

## 基于`fuck-env`这个库，开发过程支持自定义本地构建的环境变量
1. 在package.json中的config增加需要的环境变量缺省的key和vulue值
2. 在项目根目录的.env中文件中可以根据需要，动态修改环境变量的值，来达到不同的构建结果
3. 模板中缺省的变量参数说明
- static_domain 缺省是true，用于构建test/sandbox/prod版本时，代码中引用的静态资源是否添加静态资源域名，当想构建一个本地测试版本（请求的静态资源不是服务器上而是本地文件）时，static_domain置为false，然后以dist目录作为webroot在本地测试线上版本的逻辑；
- eslint_fix 缺省是false，用于在eslint代码时是否自动修复不符合规则的代码；有时候自动fix可能带来意外的bug，默认关闭。
