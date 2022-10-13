---
title: react下run build本地空白网页问题解决
tag:
- react
---

react构建项目到部署流程
```cmd
%创建项目%
npx create-react-app my-app
%进入目录%
cd my-app
%本地预览%
npm start
%打包发布%
npx run build
```
但是发现直接打开index.html界面是一片空白  
此时控制台信息
```cmd
> my-app@0.1.0 build D:\Program Files\nodejs\my-app
> react-scripts build
Creating an optimized production build...
Compiled successfully.
File sizes after gzip:
  36.94 KB  build\static\js\main.a0b7d8d3.js
  299 B     build\static\css\main.c17080f1.css
The project was built assuming it is hosted at the server root.
You can control this with the homepage field in your package.json.
For example, add this to build it for GitHub Pages:
  "homepage" : "http://myname.github.io/myapp",
The build folder is ready to be deployed.
You may serve it with a static server:
  npm install -g serve
  serve -s build
Find out more about deployment here:

  http://bit.ly/2vY88Kr
```
注意到
```cmd
The project was built assuming it is hosted at the server root.
You can control this with the homepage field in your package.json.
For example, add this to build it for GitHub Pages:
  "homepage" : "http://myname.github.io/myapp",
```
也就是说默认为你的是一个web服务器,所以生成的index.html文件中的路径如下:
```
<script type="text/javascript" src="/static/js/main.a0b7d8d3.js">
```
我们可以通过修改package.json文件的homepage属性来修改,我们打开项目根目录下的package.json,发现没有homepage这个属性,这个时候就需要我们手动加上去,如下:
```json
{
  "name": "my-app",
  "version": "0.1.0",
  "private": true,
  "homepage":"./",//手动添加
  "dependencies": {
    "react": "^16.4.1",
    "react-dom": "^16.4.1",
    "react-scripts": "1.1.4"
  },
  "scripts": {
    "start": "react-scripts start",
    "build": "react-scripts build",
    "test": "react-scripts test --env=jsdom",
    "eject": "react-scripts eject"
  }
}
```
此时我们在npm run build,你会发现index.html中的路径变了,再打开index.html就可以正常显示了!