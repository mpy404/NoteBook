# Gitbook的搭建

1. 安装node.js【我用的node10.23版本】

   - 安装好后`cmd`下输入`node -v` `npm -v`查看是否安装成功

2. npm安装gitbook

   - cmd下输入`npm install gitbook-cli -g`
   - 安装好后输入 `gitbook -V` 【可能还会安装，可能是因为node新版本的一些问题，倒退一个或两个版本就可以解决】

3. 找到合适的地方创建笔记

   - 在笔记目录下打开`cmd`，输入`gitbook init`【初始化】
   - 成功的话会生成两个文件`README.md`和`SUMMARY.md`
   - 输入`gitbook serve`会开启此服务，提醒浏览器输入`localhost:4000`来查看文档
   - 再次输入`gitbook build`【编译】会出现`_book`，可以使用该命令生成网页而不开启服务

4. 配置book.jsom

   ```json
   {
       "title" : "Java",
       "author" : "Mpy",
       "language" : "zh-hans",
       "gitbook": "3.x.x",
       "plugins": [
           "back-to-top-button", // 回到顶部
           "expandable-chapters", // 可扩展章节
           "code", // 添加行号 复制按钮
           "-lunr", "-search", "search-pro", // 高级搜索
           "github", // 添加github图标
           "splitter", // 侧边栏宽度调节
           "popup", // 新页面查看大图
           "ancre-navigation" // 页面右上角悬浮导航以及回到顶部按钮
       ]
   }
   ```

   

   