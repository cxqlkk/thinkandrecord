1. node 官网下载 mac 版 node (下载完都不用配置就好了，mac 还是挺方便的)

2. 安装vue 3  npm install -g @vue/cli

3. npm install vue-init

4. vue init mpvue/mpvue-quickstart wxapp

5. cd wxapp

6. npm install

7. npm run dev

8. 直接通过 git 下载 Vant Weapp 源代码，并将`dist`目录拷贝到自己的项目中

9. ```
   {
     "usingComponents": {
       "van-button": "/path/to/vant-weapp/dist/button/index"
     }
   }
   
   // 小程序助手将es6 转为es5
   ```

10. npm install 出现权限 不足  后面加–no-optional 