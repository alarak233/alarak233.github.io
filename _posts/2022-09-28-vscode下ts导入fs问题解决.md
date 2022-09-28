---
title: typescript引入@types/node下的模块时，编辑器报错提示找不到对应模块解决方法
tag:
- ts
---

### 报错原因可能有以下几部分:

#### **1.本地没有 @types/node声明文件包**
解决方法：  
```powershell  
npm install @types/node --save-dev
```  
#### **2.本地node_modules已经存在@types/node包，还是找不到对应的fs模块的情况**  
**解决方法：**  
检查typescript对应的编译配置文件tsconfig.json中是否配置了对应的声明包文件（@types/node），绝大可能是因为没有配置  
**配置方法如下：**  
在types下写入对应的包名（node）
```tsconfig.json
  "types": [
      "webpack-env",
      "mocha",
      "chai",
      "node"
    ]
```