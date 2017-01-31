# vue-cli_webpack-simple_firebase

> A Vue.js project

### Build Setup

``` bash
# 準備
npm install -g firebase-tools vue-cli

# プロジェクト作成
vue init webpack-simple vue-cli_webpack-simple_firebase -y

# プロジェクト内に移動
cd vue-cli_webpack-simple_firebase

# npmインストール
npm install

# firebaseとwebpack追加プラグインのインストール
npm install -S firebase CopyWebpackPlugin

# firebase初期設定
firebase init
```

### webpack.config.jsを編集
CopyWebpackPluginを追加する

```diff
# webpack.config.js
 var path = require('path')
 var webpack = require('webpack')
+var CopyWebpackPlugin = require('copy-webpack-plugin')

# ～ 省略 ～

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
+   }),
+   new CopyWebpackPlugin([
+     { from: './src/index.html' },
+     { from: './src/logo.png' }    # このpngはvue-cliによって自動で作られた画像なので、開発スタートすると不要になるので、この行は消してよい
+   ])
  ])
}
```

### 仕上げ

```bash
mv index.html src/index.html

# serve with hot reload at localhost:8080
# ブラウザにlocalhost:8080/が開き「Welcome to Your Vue.js App」が表示される
npm run dev

# build for production with minification
npm run build
```