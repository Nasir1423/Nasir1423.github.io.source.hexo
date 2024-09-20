# yiTuWorld

## 建站步骤

> 注意：一切开始之前，确保电脑已安装 `Git` 和 `Node.js`

> 注意：以下的 **Hexo 根目录**指的是**你所创建的博客项目的根目录**，同时，只要没特别说明，所有命令的执行位置为 Hexo 根目录

> 参考
>
> - [Github+picGo 搭建图床](https://zhuanlan.zhihu.com/p/489236769)
>
> - [GitHub+Hexo 搭建个人网站详细教程](https://zhuanlan.zhihu.com/p/26625249)
> - [快速搭建个人博客](https://pdpeng.github.io/2022/01/19/setup-personal-blog)
> - [Hexo 中文文档](https://hexo.io/zh-cn/)
> - [Butterfly 安装文档(一) 快速开始](https://butterfly.js.org/posts/21cfbf15/)

### Step1. 安装 [Hexo](https://hexo.io/zh-cn/)

```bash
npm install -g hexo-cli # 命令执行位置：任意
```

> Hexo 是一个快速、简洁且高效的博客框架

### Step2. 初始化项目

```bash
hexo init <your-project-name> # 命令执行位置：你的博客项目所处的路径，your-project-name 是自定义的博客名
cd <your-project-name>
npm install # 为你的博客项目安装依赖包
```

> hexo 项目文件简要解释
>
> ```bash
> .
> ├── _config.yml # 网站配置文件（themes 问价夹下的每个主题中的 _config.yml 文件称之为主题配置文件）
> ├── package.json # 应用配置文件
> ├── scaffolds # 模板文件夹。新建文章时，Hexo 会根据 scaffolds 创建文件
> ├── source # 资源文件夹。存放用户资源，除了 _post 文件夹外，所有开头命名为 _ 的文件夹/文件都会被忽略。
> |   ├── _drafts
> |   └── _posts # .md 和 .html 文件会被解析并放到 public 文件夹，其他则是直接被拷贝过去
> └── themes # 主题文件夹。Hexo 根据主题生成静态页面。
> ```

### Step3. 本地预览项目

```bash
hexo server
```

> `hexo server` 启动一个本地服务器，用于预览 Hexo 生成的静态网站。默认通过 `http://localhost:4000/` 访问网站。
>
> `hexo server -p 5000` 自定义本地服务器的端口号为 5000，此时通过 `http://localhost:5000/` 访问网站。
>
> `hexo server -s` 只使用静态文件启动本地服务器，这意味着，Hexo 不会监听文件的变动，也不会重新生成文件。
>
> `hexo server -l` 启动日志记录功能，可以通过这个选项看到 Hexo 运行时的详细日志，比如哪些文件被加载，是否有错误等。

### Step4. 配置主题 [Butterfly](https://butterfly.js.org/posts/21cfbf15/)

1. 安装：在 Hexo 根目录下执行以下命令

   ```bash
   git clone -b master https://github.com/jerryc127/hexo-theme-butterfly.git themes/butterfly
   ```

   > 执行命令后，`themes` 文件夹下出现了 `butterfly` 主题文件夹

2. 配置：修改 Hexo 根目录下的 `_config.yml`，把主题改为 butterfly

   ```yaml
   theme: butterfly
   ```

3. 安装插件

   ```bash
   npm install hexo-renderer-pug hexo-renderer-stylus --save
   ```

4. 预览主题

   ```bash
   hexo server
   ```

> 可选的操作：在 Hexo 根目录下创建 `_config.butterfly.yml` 文件，作为 Butterfly 主题的配置文件，其会覆盖掉 `themes/butterfly/_config.yml` 配置文件的同名配置。这样做有利于减少主题更新后可能带来的不便。

### Step5. 配置图床 [PicGo + GitHub + Typora](https://zhuanlan.zhihu.com/p/489236769)

> 图床是指将本地图片上传到 Github 或 Gitee 等仓库，并允许通过链接访问，这样一来，每个文章的体积将会大大减小。

> 注意：这一步要求你下载 `PicGo` 和 `Typora`

1. **新增一个 GitHub 仓库**，用于图片的存储。

   <img src="https://cdn.jsdelivr.net/gh/Nasir1423/blog-img@main/image-20240914202656679.png" alt="image-20240914202656679" style="zoom: 33.5%;" />

   <img src="https://cdn.jsdelivr.net/gh/Nasir1423/blog-img@main/image-20240914202739628.png" alt="image-20240914202739628" style="zoom:27%;" />

   <img src="https://cdn.jsdelivr.net/gh/Nasir1423/blog-img@main/image-20240914202838963.png" alt="image-20240914202838963" style="zoom:27%;" />

2. **生成该仓库的 token**，用于 PicGo 访问该图床仓库。

   <img src="https://cdn.jsdelivr.net/gh/Nasir1423/blog-img@main/image-20240914203052763.png" alt="image-20240914203052763" style="zoom: 27%;" />

   <img src="https://cdn.jsdelivr.net/gh/Nasir1423/blog-img@main/image-20240914203139516.png" alt="image-20240914203139516" style="zoom:27%;" />

   <img src="https://cdn.jsdelivr.net/gh/Nasir1423/blog-img@main/image-20240914204757860.png" alt="image-20240914204757860" style="zoom:27%;" />

   <img src="https://cdn.jsdelivr.net/gh/Nasir1423/blog-img@main/image-20240914205015674.png" alt="image-20240914205015674" style="zoom:27%;" />

   <img src="https://cdn.jsdelivr.net/gh/Nasir1423/blog-img@main/image-20240914205117586.png" alt="image-20240914205117586" style="zoom:27%;" />

   > 注意：这里生成的 token 只显示一次，请及时复制

3. **PicGo 配置图床**，用于将本地图片上传到图床。

   <img src="https://cdn.jsdelivr.net/gh/Nasir1423/blog-img@main/image-20240914210311754.png" alt="image-20240914210311754" style="zoom: 33%;" />

   > 这里的自定义域名使用了 jsdelivr 作为 cdn 加速，原自定义域名应该是 `https://raw.githubusercontent.com/github 用户名/仓库名`

4. **Typora 继承 PicGo**，用于将本地图片通过粘贴的方式，通过 PicGo 快速上传到图床。

   <img src="https://cdn.jsdelivr.net/gh/Nasir1423/blog-img@main/image-20240914210937076.png" alt="image-20240914210937076" style="zoom:27%;" />

   > 至此，在 Typora 中粘贴图片时，会通过 PicGo 自动将其上传至 GitHub 图床。

### Step6. 项目部署 GitHub Pages

> 项目部署指的是将博客项目托管到 GitHub 仓库，同时以 `username.github.io` 为 GitHub 仓库命名，这样一来，可以利用 GitHub Pages 提供的服务展示 Hexo 产生的静态文件 —— 即博客项目。

1. **创建一个 GitHub 仓库**，用于托管博客项目。这里的仓库名必须为 `username.github.io`，`username` 即你的 GitHub 用户名。

   <img src="https://cdn.jsdelivr.net/gh/Nasir1423/blog-img@main/image-20240915134328862.png" alt="image-20240915134328862" style="zoom:27%;" />

   <img src="https://cdn.jsdelivr.net/gh/Nasir1423/blog-img@main/image-20240915134353791.png" alt="image-20240915134353791" style="zoom:27%;" />

2. 如果是第一次在电脑上使用 Git，则需要**配置 SSH 公钥**，用于本地向 GitHub 推送时的验证。

   - Git Bash 中配置 Git 信息

     ```bash
     git config --global user.name "你的 GitHub 用户名"
     git config --global user.email "你的 GitHub 注册邮箱"
     ```

   - Git Bash 中生成密钥信息，生成后的 `.ssh` 文件夹中的 `id_rsa.pub` 就是我们需要的公钥

     ```bash
     ssh-keygen -t rsa -C "你的 GitHub 注册邮箱"
     ```

   - 在 [SSH and GPG keys](https://github.com/settings/keys) 新建 SSH key，标题（Key）可以任意设置，公钥（Key）的内容即上一步的 `id_rsa.pub` 中的内容，粘贴进去即可。

   - 在 Git Bash 中检测 GitHub 公钥是否设置成功

     ```bash
     ssh git@github.com
     ```

3. **修改 Hexo 根目录下的 _config.yml 配置文件**，使得 Hexo 可以和 GitHub 相关联。

   ```bash
   deploy: # 项目发布/部署配置，让 Hexo 知道将当前博客项目部署在那个位置
     type: git
     repo: https://github.com/Nasir1423/Nasir1423.github.io.git
     branch: main
   ```

4. **安装部署插件**，便于 Hexo 将静态文件上传到 GitHub 仓库。

   ```bash
   npm install hexo-deployer-git --save
   ```

5. 在 Hexo 根目录下执行以下命令，**将本地静态文件（即 public 文件夹下的内容）上传到 GitHub 仓库**。

   ```bash
   hexo clean # 清除缓存文件 (db.json) 和已生成的静态文件 (public)。
   hexo generate # 生成静态文件。
   hexo deploy # 部署你的网站。
   ```

> 至此，可以通过 `username.github.io` 这个网址访问到基于 GitHub Pages 部署的博客项目了。

### Step7. 域名配置  - 阿里云

> 根据以上步骤，你已经可以通过 `username.github.io` 这个网址访问你部署在 GitHub Pages 上的博客项目了，如果你需要使用自定义的域名访问你的博客项目，那么就需要购买自定义域名并进行配置。

1. **[在阿里云选中域名 - 购买 - DNS 解析](https://dc.console.aliyun.com/#/overview)**

   <img src="https://cdn.jsdelivr.net/gh/Nasir1423/blog-img@main/image-20240915151431014.png" alt="image-20240915151431014" style="zoom:27%;" />

2. **在托管博客项目的 GitHub 仓库中配置自定义的域名**

   <img src="https://cdn.jsdelivr.net/gh/Nasir1423/blog-img@main/image-20240915151839311.png" alt="image-20240915151839311" style="zoom:27%;" />

   <img src="https://cdn.jsdelivr.net/gh/Nasir1423/blog-img@main/image-20240915151901373.png" alt="image-20240915151901373" style="zoom:27%;" />

## Hexo 使用

### 1. 新建文章/页面

```bash
hexo new [layout] <title> # 用于创建新的文章或页面。
```

1. `[layout]` 表示要创建的文章的**布局类型**。

   - Hexo 有三种默认布局：`post`、`page`、`draft`，不同布局下创建的文件被归属于不同的路径。
     - `post` 布局：在 `source/_post` 路径下创建一个新的 `<title>.md` 文件，表示一个**博客文章**。
     - `page` 布局：在 `source/` 路径下创建一个新的 `<title>/` 文件夹，并在其中生成一个 `index.md` 文件，表示一个**独立页面**。
     - `draft` 布局：在 `source/_drafts` 路径下创建一个新的 `<title>.md` 文件，表示一个**自定义布局**。

   - 如果不指定 `layout`，则 `post` 是默认布局。默认的布局可以通过 `_config.yml` 的 `default_layout` 配置项来更改。

   - Hexo 使用的布局即对应 `scaffolds` 文件夹下的模板文件。

2. `<title>` 表示要创建的文章的**标题**。

   - 一般来说，最终创建的文件名为 `<title>.md`，但是也可以通过修改 `_config.yml` 的 `new_post_name` 配置来改变创建的文件的文件名。
   - 默认的文件名是 `<title>.md`，是因为 `new_post_name` 的默认取值是 `:title.md`，这里的 `:title` 是一个占位符，表示文章标题（小写，空格被段横杠代替）。
   - 除了 `:title` 之外，其他可选的占位符有 `:year`、`:month`、`:i_month`、`:day`、`:i_day`。以 `i_` 开头的占位符表示的月份或日期**无前导零**。

> `draft` 布局的进一步说明
>
> - 以 `draft` 布局创建的文件被保存在 `source/_drafts` 路径下，对应的文件可称之为**草稿**。
> - 可以使用 `hexo publish "My Draft Post"` 将草稿发布，或者说将草稿移动到 `source/_post` 路径下。
> - 默认情况下，草稿是不会显示在生成的站点中的。除非，
>   - 预览或生成页面时使用 `--draft` 选项，如 `hexo server --draft`
>   - 在 `_config.yml` 配置文件中设置 `render_drafts: true`
>
> ---
>
> `scaffold` 文件夹的进一步说明：上边已经说了，`scaffolds` 文件夹中的文件就是新建文章时所使用的布局。需要注意的是，你可以自定义你的模板文件/布局，并且其中可以使用三个变量：`layout`（表示布局），`title`（表示标题），`date`（表示文件建立日期）。可以通过 `{{ title }}` 的方式在模板中使用变量。
>
> ---
>
> Hexo 支持的格式的进一步说明：Hexo 支持以任意格式书写文章，但是需要安装对应的渲染插件。Hexo 会根据文件的扩展名使用不同的插件对其进行渲染。
>
> - `hexo-renderer-marked`，默认安装的插件，用于渲染 MarkDown 文件
> - `hexo-renderer-ejs`，默认安装的插件，用于渲染 EJS 文件

### 2. Front-matter

Front-matter 是每个文件开头的 YAML 或 JSON 代码块，用于**对文章进行写作配置**。以 YAML 语法表示的 Front-matter 支持的所有配置如下，

```yaml
---
# 布局，默认为 _config.yml 文件的 default_layout 的值。如果 layout: false，则表示该文章将不会使用任何布局进行渲染，但仍然会被相应的渲染引擎渲染为 HTML，"标签插件"也仍然会被处理。
layout: post 
# 标题，即文章的文件名
title: my post 
# 文件建立日期
date: 2013/7/13 20:46:25
# 文件更新日期
updated: 2013/9/13 20:46:25 
# 是否开启文章的评论功能
comments: true 
# 标签（不适用于分页）
tags: xxx 
# 分类（不适用于分页）
categories: xxx 
# 该配置项用于指定文章的永久链接
# 默认情况下，该配置项的取值为 null，此时 Hexo 会使用默认的 permalink 规则生成每篇文章的链接，如通过 https://Nasir1423.github.io/2024/09/15/my-first-post/ 就可以访问到当前文章
# 该配置项取值是一个永久链接，以 / 或 .html 结尾，如取值为 /my-first-post/ 时，可以通过 https://Nasir1423.github.io/my-first-post/ 的方式访问到当前文章
permalink: /my-fitst-post/ 
# 纯文本的页面摘要，也可以使用"标签插件"来格式化文本
# 注：标签插件是 Hexo 提供的功能，允许在 MarkDown 中使用特定的标签和语法来实现图片插入等功能
excerpt: xxx 
# 是否禁用 Nunjucks 标签（类似于插值语法，通过 {{}} 或 {%%} 的方式解析变量）和"标签插件"的渲染
disableNunjucks: false 
# 语言，默认为 _config.yml 文件的 language 的值
lang: zh-hans 
# 文章是否发布，对于 source/_post 文件夹下的文章其取值为 true，对于 source/_draft 文件夹下的文章其取值为 false
published: true 
---
```

> 关于标签 `tags` 和分类 `categories` 的说明
>
> 1. `tags`：用于**对文章进行标记的关键词，平级结构**。所有标签处于**同一层级**，同时它也是**没有顺序的**。
>
> 2. `categories`：用于**组织文章的层次结构**。分类支持**多级结构**，同时它是**有顺序**的。
>
> ```yaml
> tags: # 表示当前文章包含三个关键词 Injury、Fight、Shocking
>   - Injury
>   - Fight
>   - Shocking
> ```
>
> ```yaml
> categories: # 表示当前文章属于 Sports 大类别下的 BaseBall 小类别
>   - Sports
>   - Baseball
> ```
>
> ```yaml
> categories: # 多层次分类，表示当前文章属于
>   - [Sports, Baseball] # 表示当前文章属于 Sports（体育）大类别下的 Baseball（棒球）小类别
>   - [MLB, American League, Boston Red Sox] # 表示当前文章属于 MLB（美国职业棒球大联盟）大类别下的 American League（美联）中类别的 Boston Red Sox（波士顿红袜队）
>   - [MLB, American League, New York Yankees] # 表示当前文章属于 MLB（美国职业棒球大联盟）大类别下的 American League（美联）中类别的 New York Yankees（纽约洋基队）
>   - Rivalries # 表示当前文章属于 Rivalries（对抗）类别
> ```

#### 2.1 Butterfly

对于 Butterfly 主题，有两种 Front-matter：用于页面（page layout）配置的 Page Front-matter 和用于文章页（post/draft layout）配置的 Post Front-matter。

##### 2.1.1 Page Front-matter

```yaml
---
title: # 【必需】页面标题
date: # 【必需】页面创建日期
updated: # 【可选】页面更新日期
type: # 【必需】标签、分类和友情链接三个页面需要配置
comments: # 【可选】显示页面评论模块 (默认 true)
description: #【可选】页面描述
keywords: # 【可选】页面关键字
top_img: # 【可选】页面顶部图片
mathjax: # 【可选】显示 mathjax (当设置 mathjax 的 per_page: false 时，才需要配置，默认 false)
katex: # 【可选】显示 katex (当设置 katex 的 per_page: false 时，才需要配置，默认 false)
aside: # 【可选】显示侧边栏 (默认 true)
aplayer: # 【可选】在需要的页面加载 aplayer 的 js 和 css,请参考文章下面的音乐 配置
highlight_shrink: # 【可选】配置代码框是否展开 (true/false) (默认为设置中 highlight_shrink 的配置)
random: # 【可选】配置友情链接是否随机排序（默认为 false)
---
```

##### 2.1.2 Post Front-matter

```yaml
---
title: # 【必需】文章标题
date: # 【必需】文章创建日期
updated: # 【可选】文章更新日期
tags: # 【可选】文章标签
categories: # 【可选】文章分类
keywords: # 【可选】文章关键字
description: # 【可选】文章描述
top_img: # 【可选】文章顶部图片
comments: # 【可选】显示文章评论模块 (默认 true)
cover: # 【可选】文章缩略图 (如果没有设置 top_img, 文章页顶部将显示缩略图，可设为 false/图片地址/留空)
toc: # 【可选】显示文章 TOC (默认为设置中 toc 的 enable 配置)
toc_number: # 【可选】显示 toc_number (默认为设置中 toc 的 number 配置)
toc_style_simple: # 【可选】显示 toc 简洁模式
copyright: # 【可选】显示文章版权模块 (默认为设置中 post_copyright 的 enable 配置)
copyright_author: # 【可选】文章版权模块的文章作者
copyright_author_href: # 【可选】文章版权模块的文章作者链接
copyright_url: # 【可选】文章版权模块的文章连结链接
copyright_info: # 【可选】文章版权模块的版权声明文字
mathjax: # 【可选】显示 mathjax (当设置 mathjax 的 per_page: false 时，才需要配置，默认 false )
katex: # 【可选】显示 katex (当设置 katex 的 per_page: false 时，才需要配置，默认 false )
aplayer: # 【可选】在需要的页面加载 aplayer 的 js 和 css,请参考文章下面的音乐 配置
highlight_shrink: # 【可选】配置代码框是否展开 (true/false) (默认为设置中 highlight_shrink 的配置)
aside: # 【可选】显示侧边栏 (默认 true)
abcjs: # 【可选】加载 abcjs (当设置 abcjs 的 per_page: false 时，才需要配置，默认 false )
---
```

### 3. Butterfly - 创建页面

#### 3.1 创建标签页

Step1. 在 Hexo 根目录下执行命令 `hexo new page tags`

Step2. 修改新增的 `source/tags/index.md` 文件的内容为

```markdown
---
title: 标签
date: 2024-09-15 20:56:23
type: "tags" # 【必须】页面类型，必须为 tags
orderby: random #【可选】排序方式，可选 random/name/length
order: 1 #【可选】排序次序，可选 1 表示升序，-1 表示降序
---
```

> 可以通过 `/tags` 的方式访问到该标签页

#### 3.2 创建分类页

Step1. 在 Hexo 根目录下执行命令 `hexo new page categories`

Step2. 修改新增的 `source/categories/index.md` 文件的内容为

```markdown
---
title: 分类
date: 2024-09-15 21:00:20
type: "categories"
---
```

> 可以通过 `/categories` 的方式访问到该分类页

#### 3.3 创建友情链接

Step1. 在 Hexo 根目录下执行命令 `hexo new page link`

Step2. 修改新增的 `source/link/index.md` 文件的内容为

```markdown
---
title: 友情链接
date: 2024-09-15 21:01:52
type: "link"
---
```

Step3. 添加友情链接

- 方式一：本地添加，创建 `source/_data/link.yml` 文件，用于存储友情链接信息

  ```yaml
  - class_name: 友情链接
    class_desc: 那些人，那些事
    link_list:
      - name: Hexo
        link: https://hexo.io/zh-tw/
        avatar: https://d33wubrfki0l68.cloudfront.net/6657ba50e702d84afb32fe846bed54fba1a77add/827ae/logo.svg
        descr: 快速、简单且强大的网志框架
  
  - class_name: 网站
    class_desc: 值得推荐的网站
    link_list:
      - name: Youtube
        link: https://www.youtube.com/
        avatar: https://i.loli.net/2020/05/14/9ZkGg8v3azHJfM1.png
        descr: 视频网站
      - name: Weibo
        link: https://www.weibo.com/
        avatar: https://i.loli.net/2020/05/14/TLJBum386vcnI1P.png
        descr: 中国最大社交分享平台
      - name: Twitter
        link: https://twitter.com/
        avatar: https://i.loli.net/2020/05/14/5VyHPQqR6LWF39a.png
        descr: 社交分享平台
  ```

- 方式二：远程拉取，即在 `source/link/index.md` 的 front-matter 中通过 `flink_url` 添加远程链接

  ```mark
  flink_url: xxxxxx
  ```

  > 注意：远程拉取只支持 json，同时本地添加友情链接的方法将会失效

  > 注意：支持通过 front-matter 的 `random: true` 配置，使得**友情链接随机排序**；支持通过 `source/link/index.md` 的方式**自定义友情链接页面**

> 可以通过 `/link` 的方式访问到该友情链接页

### 4. Butterfly - 主题配置

#### 4.1 _config.yml

> `_config.yml` 是站点配置文件

```yaml
language: zh-CN # 语言，Butterfly 主题关于该配置支持三种选项，en(默认值，英文)、zh-CN(简体中文)、zh-TW(繁体中文)
```

#### 4.2 _config.butterfly.yml

> `_config.butterfly.yml` 是 butterfly 主题配置文件，比 `themes/butterfly/_config.yml` 主题配置文件优先级更高

##### 4.2.1 导航栏配置

##### 4.2.2 1212

##### 4.2.3 121212

### 5. Hexo 项目的管理







