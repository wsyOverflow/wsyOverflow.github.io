# 1 说明

本仓库用于hexo搭建个人博客主页 https://wsyoverflow.github.io/

# 2 hexo安装

1. 自行安装 Node.js
2. 安装 hexo 命令行工具
   ```bash
   npm install -g hexo-cli 
   ```

3. 手动下载安装 pandoc：https://pandoc.org/installing.html

4. 安装 hexo-render-pandoc

   ```bash
   npm install hexo-renderer-pandoc --save
   ```


# 3 hexo配置

hexo个人博客配置主要参考了 [使用 Hexo 搭建个人博客](https://kiku.vip/2020/12/21/Hexo/#%E4%B8%BA%E4%BB%80%E4%B9%88%E8%A6%81%E6%90%AD%E5%BB%BA%E4%B8%AA%E4%BA%BA%E5%8D%9A%E5%AE%A2) 。

hexo 根目录下`_config.yml`文件的相关配置：

- hexo发布会清除本仓库文件，为了保留readme。设置`skip_render`跳过 README.md 文件。以及忽略掉 draf
  ```yaml
  skip_render:
    - README.md
    - draft/**/*
    - images/draft/**/*
  ```

- 安装图片路径处理插件
  ```
  npm install --save hexo-asset-image
  ```

  并在`_config.yml`配置  `post_asset_folder: true`

markdown编辑器采用typora，直接在 `source/_posts` 目录写markdown博客，图片根目录为 `source/images`。

为了方便版本控制文档源文件，可以在另一目录中写markdown，软连接到 source 文件夹。

# 4 typora 配置

为了支持不同层级目录，统一图片存储路径 `[/path/to/hexo]/source/images`，打开 typora偏好设置 > 图像：
- 图片语法偏好：选中 `优先使用相对路径` 和 `插入时自动转义图片URL`

在每个文档中配置 Front-matter，主要配置：

- `typora-copy-images-to`：插入图片时，图片的保存位置。与 typora偏好设置>图像>插入图片时 里设置的路径同样的作用，只是这里只对当前文档生效。

-  `typora-root-url` 属性，根据当前文档相对于图片根目录的相对路径进行设置。

  以 `source/_posts/Paper-Notes/` 下的一篇文档为例，设置

```yaml
typora-copy-images-to: ..\..\..\images\Paper Notes\${filename}
typora-root-url: ..\..\..\
```

# 5 更新

在hexo根目录 `/path/to/hexo` 打开终端

## 5.1 本地调试

正式发布前可以先本地调试看看效果

```bash
#根据 Markdown 文档生成博客静态文件，可以简写成 hexo g
hexo generate

#在本地启动一个 http 服务器，默认情况下，访问网址为： http://localhost:4000/
hexo server
```

## 5.2 部署

执行过 hexo g 后即可部署到github主页

```bash
hexo deploy -m "commit message"
```

# 6 图片问题

本文档采用的是绝对路径形式的图片路径，理论上网页上图片 url 应该是 /images/path/to/file。有时候刷新或者换个浏览器会好

如果以上配置都正确，但图片url就是不对，那就新起目录重新配置
