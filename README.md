## 说明

本仓库用于hexo搭建个人博客主页 https://wsyoverflow.github.io/

### hexo安装

1. 自行安装 Node.js
2. 安装 hexo 命令行工具
   ```bash
   npm install -g hexo-cli 
   ```

3. 安装 hexo-render-pandoc
   
   先安装 pandoc：https://pandoc.org/installing.html
   
   ```bash
   npm install hexo-renderer-pandoc --save
   ```
   

## hexo配置

hexo个人博客配置主要参考了 [使用 Hexo 搭建个人博客](https://kiku.vip/2020/12/21/Hexo/#%E4%B8%BA%E4%BB%80%E4%B9%88%E8%A6%81%E6%90%AD%E5%BB%BA%E4%B8%AA%E4%BA%BA%E5%8D%9A%E5%AE%A2) 。

hexo 根目录下`_config.yml`文件的相关配置：

- hexo发布会清除本仓库文件，为了保留readme。设置`skip_render`跳过 README.md 文件
  ```yaml
  skip_render:
    - README.md
  ```

markdown编辑器采用typora，直接在 `source/_posts` 目录写markdown博客，图片根目录为 `source/images`。

### typora图片路径

为了支持不同层级目录统一图片存储路径 `source/images`，打开 typora偏好设置 > 图像：
- 插入图片：选择复制指定路径，
    - 路径使用绝对路径 `[/path/to/hexo]/source/images/${filename}.assets`
    - 选中 `对本地位置的图片应用上述规则` 和 `对网络位置的图片应用上述规则` 

- 图片语法偏好：选中 `优先使用相对路径` 和 `插入时自动转义图片URL`

在每个文档中设置 Front-matter 的 `typora-root-url` 属性，根据当前文档相对于图片根目录的相对路径进行设置。例如 `source/_posts/Paper-Notes/` 下的一篇文档，则设置
```
typora-root-url: ../../
```

## 部署

在hexo根目录 `/path/to/hexo` 打开终端

### 本地调试

正式发布前可以先本地调试看看效果

```bash
#根据 Markdown 文档生成博客静态文件，可以简写成 hexo g
hexo generate

#在本地启动一个 http 服务器，默认情况下，访问网址为： http://localhost:4000/
hexo server
```

### 部署

执行过 hexo g 后即可部署到github主页

```bash
hexo deploy -m "commit message"
```

