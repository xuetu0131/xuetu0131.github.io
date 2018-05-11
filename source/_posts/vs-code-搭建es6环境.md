---
title: vs code 搭建es6环境
date: 2018-05-09 15:42:01
tags: [vscode,nodejs,babel]
categories: [coding]
---
## vscode 中搭建es6变成环境
### 1. babel安装
```
npm install babel-cli --save-dev
```
修改package.json 再`script`标签中添加
```
//将src中的文件babel处理之后输出到lib文件夹
"build": "babel src -d lib"
```
### 2. 设置preset安装pulgin
安装babel-preset-env用于将不同的语法转换为es5
```
npm install babel-preset-env --save-dev
```
新建`.babelrc`文件，并修改
```
{
  "presets": ["env"],
  "plugin" : []
}
```
安装async await插件
```
npm install --save-dev babel-plugin-transform-runtime
```
在`.babelrc`文件的plugin中添加
```
"plugins": [  "transform-runtime"]
```
### 3. 完成
接下来就可以通过`npm run build`完成转码`node ./lib/filename.js`来运行