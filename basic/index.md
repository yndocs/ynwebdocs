# 快速开始
  安装ember指令<br>
  ~~~
  npm install -g ember-cli@2.7
  ~~~

## 创建新项目
  ~~~
  ember new ember-quickstart
  ~~~
  `ember-quickstart` 为所要创建ember项目的项目名

## 创建路由
  ~~~
  ember generate route scientists
  ~~~
  `scientists` 为所要创建的路由器名称

## 创建控制器
  ~~~
  ember generate controller scientists
  ~~~
  `scientists` 为所要创建的控制器名称

## 创建组件
  ~~~
  ember generate component people-list
  ~~~
  `people-list` 为所要创建的组件名称

## 创建工具类助手
  ~~~
  ember generate helper my-helper
  ~~~
  `my-helper` 为所要创建的工具类助手名称


## 运行ember系统
  ~~~
  ember server -proxy https://dev.ynkjy.com
  ~~~
  其中`https://dev.ynkjy.com`为后端服务器地址
## 项目打包
  ~~~
  ember build -prod
  ~~~
  通过指令在项目所在目录上生成dist文件，这个文件为打包出来的前端包