---
title: Hexo + Butterfly 建站记录
date: 2024-09-24 17:19:19
tags:
  - Hexo
  - 个人博客
description: 基于 Hexo + Butterfly 构建个人博客网站，该贴文涵盖 1. 保姆式的建站步骤 2. Hexo 博文发布与管理 3. Butterfly 主题的相关配置 4. Hexo 项目管理 5. Butterfly 标签外挂的基本使用。存在疑问？在评论区留言吧！
---
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

### 4. Butterfly - 主题配置 1

#### 4.1 _config.yml

> `_config.yml` 是站点配置文件

```yaml
language: zh-CN # 语言，Butterfly 主题关于该配置支持三种选项，en(默认值，英文)、zh-CN(简体中文)、zh-TW(繁体中文)
```

#### 4.2 _config.butterfly.yml

> `_config.butterfly.yml` 是 butterfly 主题配置文件，比 `themes/butterfly/_config.yml` 主题配置文件优先级更高

##### 4.2.1 导航栏配置

```yaml
nav: # 注意，这里的导航栏指的是网页顶层用于快速导航的区域
  logo: "images/butterfly_nav_logo.svg" # （导航栏）logo，注意：这里的根目录是 /source/
  display_title: true # （导航栏）是否显示网站标题，可选 true/false
  fixed: false # （导航栏）是否固定，可选 true/false

# Menu (菜单设置)
menu: # 注意，这里的菜单指的是导航栏右上角的快速导航
  # 1. 菜单的语法必须是：/xxx/，后面 || 分开，然后写图标名。
  # 2. Home 目录的解释为，其他类似
  #  - Home 是目录名；/ 是点击该目录后跳转的链接地址；|| 是链接地址和图标的分隔符；
  #  - fas fa-home 是 Font Awesome 图标库中的图标，fas 表示该图标库中的 solid 样式（实心），fa-home 表示该图标库中的房子图标类名
  # Home: / || fas fa-home
  # Archives: /archives/ || fas fa-archive
  # Tags: /tags/ || fas fa-tags
  # Categories: /categories/ || fas fa-folder-open
  # List||fas fa-list:
  #   Music: /music/ || fas fa-music
  #   Movie: /movies/ || fas fa-video
  # Link: /link/ || fas fa-link
  # About: /about/ || fas fa-heart
  首页: / || fas fa-home
  时间轴: /archives/ || fas fa-archive
  标签: /tags/ || fas fa-tags
  分类: /categories/ || fas fa-folder-open
  # 清单||fa fa-heartbeat:
  #   音乐: /music/ || fas fa-music
  #   照片: /Gallery/ || fas fa-images
  #   电影: /movies/ || fas fa-video
  友链: /link/ || fas fa-link
  关于: /about/ || fas fa-heart
```

##### 4.2.2 代码块设置

```yaml
highlight_theme: mac # 代码主题高亮，可选 darker / pale night / light / ocean / mac / mac light / false，也可以尝试去自定义高亮
highlight_copy: true # 是否显示复制按钮，即是否支持代码复制，可选 true/false
highlight_lang: true # 是否显示代码语言，可选 true/false
highlight_shrink: false # 是否支持代码块关闭，可选 true（代码块不展开，可以通过点击 '>' 展开）/ false（代码块展开，可以通过点击 '>' 关闭）/ none（代码块展开，同时隐藏 '>' 按钮）
# 补充说明，主题文件中可以通过 highlight_shrink 设置是否支持代码块展开，同时也可以在文章的 front-matter 中通过 highlight_shrink 来单独进行设置，并优先级更高
highlight_height_limit: 100 # 表示是否配置代码高度限制，超过部分会被隐藏。可选 number（单位是 px）/ false（不配置高度限制）
# 补充说明：配置代码高度后，实际限制的高度是 highlight_height_limit + 30px
code_word_wrap: false # 表示是否实现代码不自动换行，true 则不会让代码自动换行，从而不会在代码块区域中出现横向滚动条
# 补充说明，如果设置代码不换行，即 code_word_wrap: true，此时还要进行以下设置
# 如果 Hexo 正在使用 highlight 引擎渲染代码块，则需要修改站点配置 _config.yml 中的 highlight.line_number: false
# 如果 Hexo 正在使用 prismjs 引擎渲染代码块，则需要修改站点配置 _config.yml 中的 prismjs.line_number: false
```

##### 4.2.3 社交图标设置

```yaml
formal: # 定义社交图标的格式为 图标名: url || 描述性文字 || color
  icon: link || the description || color # icon 图标的 font awesome 类名；link 点击图标后的跳转链接；description 图标的悬停文本；color 十六进制表示的图标颜色
social:
  fab fa-github: https://github.com/Nasir1423 || Github || '#24292e' # github
  fas fa-envelope: mailto:wangjian1423@foxmail.com || 邮箱 || '##1e3050' # 邮箱
```

##### 4.2.4 图片设置

```yaml
favicon: /images/butterfly_favicon.svg # Favicon (网站图标)
avatar: # Avatar (头像)
  img: /images/butterfly_avatar_img.svg
  effect: false # 头像是否自动旋转，可选 true（旋转）/ false（不旋转）
```

##### 4.2.5 顶部图设置

```yaml
# 这里的设置涵盖：顶部图是否显示，默认顶部图，默认 tag 子页面顶部图，默认 category 子页面顶部图，
# 主页顶部图，归档页顶部图，特定 tag 子页面顶部图，特定 category 子页面顶部图...
disable_top_img: false # 是否禁用网页顶部图，可选 true / false
# 补充说明：关于顶部图的获取顺序
# 页面的顶部图（layout === page）时，各自配置的 top_img > 配置文件的 default_top_img
# 文章的顶部图（layout === post）时，各自配置的 top_img > cover > 配置文件的 default_top_img

index_img: images/Tartaglia/1219675.jpg # 主页的顶部图。注意：文章或页面可以通过 front-matter 的 top_img 配置对顶部图进行单独设置。

default_top_img: "linear-gradient(to top, #2980b9, #6dd5fa, #ffffff);" # 默认的顶部图。当文章或页面没有通过 front-matter 的 top_img 设置顶部图时，则显示默认的顶部图。

archive_img: # 归档页的顶部图。

tag_img: # tag 子页面的的默认顶部图。如果 tag 子页面没有通过 top_img 设置顶部图，则显示默认的 tag 子页面的顶部图。
# 补充说明：tag page, not tags page

# The banner image of tag page
# format:
#  - tag name: xxxxx
tag_per_img: # 为特定的 tag 子页面设置顶部图，即配置每个 tag 的顶部图。语法见上面的 format。

category_img: # category 子页面的默认顶部图。如果 category 子页面没有通过 top_img 设置顶部图，则显示默认的 category 子页面的顶部图。
# 补充说明：category page, not categories page

# The banner image of category page
# format:
#  - category name: xxxxx
category_per_img: # 为特定的 category 子页面设置顶部图，即配置每个 category 的顶部图。语法见上面的 format。

# 补充说明：顶部图的可选值，即 xxx_yyy_image 类似字段的可选值（即设置的顶部图的可能的取值情况）
# 1. 留空：如果是页面，则显示默认的 top_image，如果没有则显示默认的颜色；如果是文章页，则显示 cover 的值。
# 2. 图片链接：表示显示所指定的图片
# 3. 颜色：可选 HEX 值（如 #0000ff），RGB 值（如 rgb(0,0,255)），颜色单词（如 orange），渐变色（如 linear-gradient(135deg, #E2B0FF 10%, #9F44D3 100%)）
# 4. transparent：表示透明
# 5. false：表示不显示 top_img
```

##### 4.2.6 封面设置

```yaml
# 补充说明-1：这里用于设置文章的默认封面，对于特定的文章，可以通过 front-matter 的 cover 字段配置封面
# 补充说明-2：封面的优先级为，front-matter 的 cover 字段 > 当前主题配置文件的 default_cover 字段 > false
cover:
  index_enable: true # 表示主页是否显示文章封面图
  aside_enable: true # 表示侧栏是否显示文章封面图
  archives_enable: true # 表示归档页面是否显示文章封面图
  position: left # 表示主页卡片文章封面的显示位置，可选 left（左边）/ right（右边）/ both（左右轮流）
  default_cover: # 表示默认的封面，可选图片链接，颜色，渐变色等
  # 补充说明：如果要默认封面生效，需要在文章的 front-matter 的 cover 字段设置为空
```

##### 4.2.7 替换无法显示的图片设置

```yaml
error_img:
  flink: /img/friend_404.gif # 友情链接页面加载失败时的默认替代图片
  post_page: /img/404.jpg # 页面或文章图片加载失败时的默认替代图片
```

##### 4.2.8 自定义的 404 页面设置

```yaml
error_404:
  enable: true # 是否启用自定义的 404 页面，可选 true / false
  subtitle: "Page Not Found" # 404 页面的副标题文字
  background: images/Other/1212121.svg # 404 页面的背景图片
```

##### 4.2.9 文章元信息设置

```yaml
post_meta:
  page: # 主页元信息
    date_type: created # 文章日期，可选 created（创建日期）/ updated（更新日期）/ both（都显示）
    date_format: date # 文章日期格式，可选 date（日期）/ relative（绝对日期）
    categories: true # 是否显示文章分类，可选 true / false
    tags: false # 是否显示文章标签，可选 true / false
    label: true # 是否显示描述性文字，可选 true / false
  post: # 其他文章元信息，解释同上
    date_type: both
    date_format: date
    categories: true
    tags: true
    label: true
```

##### 4.2.10 主页文章摘要显示设置

```yaml
index_post_content:
  method: 3 # 表示主页中文章摘要的显示方式，可选 1 / 2 / 3 / false
  # 补充说明：method 取值的具体含义
  # 1 - description，即显示文章描述，即显示文章在自身的 front-matter 中配置的 description 字段作为文章摘要
  # 2 - both，即优先显示 description，没有则显示自动生成的摘要
  # 3 - auto_excerpt（默认值），即只显示自动生成的摘要
  # false，即不显示文章摘要
  length: 500 # 表示文章摘要的长度（即字符数），如果 method 配置取值为 2 或 3，则必须配置 length 字段
```

##### 4.2.11 页面锚点设置

```yaml
anchor:
  # when you scroll, the URL will update according to header id.
  auto_update: false # 表示 URL 是否会随着滚动自动更新为当前可见的标题（header）的 id
  # Click the headline to scroll and update the anchor
  click_to_scroll: true # 表示点击标题是否会使页面滚动到该标题位置，并更新 URL
```

##### 4.2.12 图片描述文字设置

```yaml
photofigcaption: false # 表示是否开启图片描述文字显示，true 则开启，false 则关闭。优先显示图片的 title 属性，然后是 alt 属性。
```

##### 4.2.13 复制设置

```yaml
copy:
  enable: true # 表示是否开启网站的复制权限，可选 true / false
  copyright:
    enable: false # 表示是否在复制的内容后加上版权信息，可选 true / false，即 "来源: 川一土的博客视界 著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。"
    limit_count: 50 # 字数限制，即当复制的文字大于该字数限制时，才在复制的内容后边加上版权信息
```

##### 4.2.14 文章页相关设置

###### 文章版权

```yaml
post_copyright: # 文章版权，即为你的博客文章展示文章版权和许可协议
  enable: true # 表示是否显示在文章页显示文章版权信息（包括作者、链接、版权声明、协议），可选 true / false
  decode: false # 表示是否对网址进行解码，因此如果是中文网址，则可以设置 decode: true 来显示中文网址
  author_href: https://github.com/Nasir1423 # 作者的链接
  license: CC BY-NC-SA 4.0 # 版权声明中的协议
  license_url: https://creativecommons.org/licenses/by-nc-sa/4.0/ # 协议的链接
  # 补充说明 - 1：如果特定文章（如转载文章）不需要显示版权信息，则可以在文章的 front-matter 中设置 copyright: false
  # 补充说明 - 2：可以支持对单独文章设置版权信息，即通过文章的 front-matter 中通过以下字段设置
  # (1) copyright_author: xxx # 设置作者
  # (2) copyright_author_url: https://xxx.com # 设置作者链接
  # (3) copyright_url: https://xxx.com # 设置文章原始链接
  # (4) copyright_info: 此文章版权归 xxxxx 所有，如有转载，请注明来自原作者 # 设置版权信息
```

###### 文章打赏

```yaml
reward: # 文章打赏
  enable: false # 表示是否开启打赏按钮，可选 true / false
  text: # 打赏按钮的文字，默认为 "赞助"
  QR_code: # 打赏信息，每一项需要包含 img、link、text 三项
    - img: /img/wechat.jpg # 打赏二维码
      link: # 打赏链接，如果不写则默认为 img 的链接
      text: wechat # 打赏文字
    - img: /img/alipay.jpg
      link:
      text: alipay
```

###### 文章目录

```yaml
toc: # 文章目录，toc 是 table of content 的缩写
  post: true # 表示文章页（layout === post）是否显示目录
  page: false # 表示普通页面（layout === page）是否显示目录
  number: true # 表示是否显示章节数，即是否显示 1.；1.3；5.1.3 等章节标识
  expand: true # 表示是否展开目录
  style_simple: true # 表示文章页（layout === post）的侧边栏是否打开简洁模式，即侧边栏只显示目录
  scroll_percent: false # 表示是否显示滚动进度百分比
  # 补充说明：可以通过 front-matter 中的特定字段 top_number 和 toc 为特定文章配置目录的显示情况
```

###### 相关文章推荐

```yaml
related_post: # 相关文章推荐
  enable: true # 是否开启相关文章推荐
  # 补充说明 - 1：相关文章推荐的原理是根据文章 tags 的比重来推荐文章
  # 补充说明 - 2：如果被推荐的相关文章的 front-matter 中设置了 cover: false，那么相关文章的背景会显示主题色
  limit: 6 # 相关推荐文章的数目
  date_type: created # 被推荐的文章的日期类型，可选 created（创建日期）/ updated（更新日期）
```

###### 文章过期提醒

```yaml
noticeOutdate: # 文章过期提醒
  # 补充说明：文章是否过期以更新时间为基准
  enable: false # 表示是否开启文章过期提醒
  style: flat # 过期提醒的风格，可选 simple / flat
  limit_day: 500 # 表示距离更新时间多少天才显示文章过期提醒
  position: top # 表示过期提醒显示的位置，可选 top / bottom
  message_prev: It has been # 过期提醒的天数之前的文字
  message_next: days since the last update, the content of the article may be outdated. # 过期提醒的天数之后的文字
```

###### 文章编辑按钮

```yaml
post_edit: # 文章编辑按钮
  # 补充说明：当 post_edit.enable: true 时，文章标题旁边会显示一个编辑按钮，此时点击会跳转到对应的链接去
  enable: false # 表示是否开启文章的在线编辑
  # url: https://github.com/user-name/repo-name/edit/branch-name/subdirectory-name/
  # For example: https://github.com/jerryc127/butterfly.js.org/edit/main/source/
  url: # 当前文章在 GitHub 中的目录
```

###### 文章分页按钮

```yaml
post_pagination: 1 # 文章分页按钮，可选 1 / 2 / false
# 补充说明 - 1：1 表示 “下一篇” 按钮导航到旧的文章；2 表示 “下一篇” 按钮导航到新的文章；false 表示关闭分页显示
# 补充说明 - 2：如果 “下一篇” 的文章的 front-matter 设置 cover: false，那么分页背景就是主题色
```

##### 4.2.15 博客页脚设置

```yaml
footer:
  owner: # 显示博客年份和作者，如 "©2020 - 2024 By yiTuChuan"
    enable: true # 表示是否显示
    since: 2024 # 表示开始时间，即站点的起始时间
  copyright: true # 表示是否显示主题（Butterfly）和框架（Hexo）的版权信息
  custom_text: # 自定义的页脚文本，支持 HTML，这里也可以写 ICP 备案信息
```

##### 4.2.16 博客侧边栏设置

> 注意：博客的侧边栏支持[自定义](https://butterfly.js.org/posts/ea33ab97/)

###### 侧边排版

```yaml
aside: # 侧边排版
  enable: true # 是否启用侧边栏
  hide: false # 是否默认隐藏侧边栏
  button: true # 是否显示切换侧边栏的按钮
  mobile: true # 是否在移动设备上显示侧边栏
  position: right # 侧边栏的位置，可选 left / right
  display: # 是否显示特定的侧边栏设置
    archive: true # 是否显示归档侧边栏
    tag: true # 是否显示标签侧边栏
    category: true # 是否显示分类侧边栏
  card_author: # 作者信息卡片设置
    enable: true # 是否显示作者信息卡片
    description: plant your tree, now! # 作者描述信息
    button: # 关注按钮设置
      enable: true # 是否显示关注按钮
      icon: fab fa-github # 关注按钮图标
      text: follow me # 关注按钮文字
      link: https://github.com/Nasir1423 # 关注按钮跳转链接
  card_announcement: # 公告卡片
    enable: false # 是否显示公告卡片
    content: This is my Blog # 公告卡片文字
  card_recent_post: # 最近文章卡片
    enable: true # 是否显示最近文章卡片
    limit: 5 # 最近文章显示的最大数量，如果设置为 0 则表示显示全部
    sort: date # 最近文章显示的排序依据，可选 date（日期） / updated（更新时间）
    sort_order: # Don't modify the setting unless you know how it works
  card_categories: # 分类卡片
    enable: true # 是否启用
    limit: 8 # 显示的分类数量限制，如果设置为 0 则表示显示全部
    expand: none # 是否展开分类列表，可选 none / true / false
    sort_order: # Don't modify the setting unless you know how it works
  card_tags: # 标签卡片
    enable: true # 是否启用
    limit: 40 # 显示的标签数量限制，如果设置为 0 则表示显示全部
    color: false # 是否使用彩色标签
    orderby: random # 标签的排序依据，可选 random / name / length
    order: 1 # 标签的排序次序，可选 1（升序）/ -1（降序）
    sort_order: # Don't modify the setting unless you know how it works
  card_archives: # 归档卡片
    enable: true # 是否启用
    type: monthly # 按照年度还是月度归档，可选 yearly / monthly
    format: MMMM YYYY # 日期格式
    order: -1 # 归档的排序次序，可选 1（升序）/ -1（降序）
    limit: 8 # 显示的归档数量限制，如果设置为 0 则表示显示全部
    sort_order: # Don't modify the setting unless you know how it works
  card_webinfo: # 网站信息卡片
    enable: true # 是否启用
    post_count: true # 是否显示文章数量
    last_push_date: true # 是否显示最后更新日期
    sort_order: # Don't modify the setting unless you know how it works
  card_post_series: # 文章系列卡片
    enable: true # 是否启用
    series_title: true # 是否显示系列标题
    orderBy: "date" # 文章系列的排序依据， 可选 title / date
    order: -1 # 文章系列的排序次序，可选 1（升序）/ -1（降序）
```

###### 访问人数

```yaml
busuanzi: # 访问人数
  # 补充说明 - 1：busuanzi 是一个开源的网站访问量统计工具，可以统计网站的独立访客数 (UV) 和页面访问量 (PV)。
  # 它可以方便地集成到你的网站中，帮助你了解网站的访问情况。
  # 补充说明 - 2：可以通过 CDN.option.busuanzi 配置 busuanzi 的 CDN 链接
  site_uv: true # 表示是否启用网站独立访客统计
  site_pv: true # 表示是否启用网站总访问量统计
  page_pv: true # 表示是否启用页面访问量统计
```

###### 网页已运行时间

```yaml
runtimeshow: # 网页已运行时间
  # 补充说明：网页已运行时间即网页发布时间和当前时间的差值
  enable: false # 是否启用
  publish_date: # 网页发布时间，格式为 Month / Day / Year Time 或 Year / Month / Day Time
  # 发布时间示例：6/7/2018 00:00:00
```

###### 最新评论

```yaml
newest_comments: # 最新评论
  enable: false # 是否启用
  sort_order: # Don't modify the setting unless you know how it works
  limit: 6 # 最大显示数量
  storage: 10 # 缓存时间，单位是分钟，表示在缓存时间内不会调用 API 获取数据
  avatar: true # 是否显示头像
```

##### 4.2.17 右下角按钮

```yaml
translate: # 简繁转换
  enable: false # 是否启用
  default: 繁 # 按钮默认显示文字（如果网站是简体，则应设置为 '繁'，否则为 '简'）
  defaultEncoding: 2 # 网站默认语言，1 表示繁体中文，2 表示简体中文
  translateDelay: 0 # 延迟时间，即简繁切换的延迟翻译时间
  msgToTraditionalChinese: "繁" # 文字是简体时，按钮显示的文字
  msgToSimplifiedChinese: "簡" # 文字是繁体时，按钮显示的文字

readmode: true # 是否启用阅读模式按钮，该按钮只会出现在文章页，点击后进入阅读模式，阅读模式下会去除掉文章外的内容，避免干扰阅读

darkmode: # 夜间模式
  enable: true # 是否启用
  button: true # 是否显示右下角的日夜模式切换按钮
  autoChangeMode: false # 是否允许日夜模式自动切换，可选 1（跟随系统而变化）/ 2（按照配置 start 和 end 进行切换）/ false（取消自动切换）
  start: # 8，日间模式的开始时间
  end: # 22，日间模式的结束时间

rightside_scroll_percent: false # 是否在 “回到顶部” 按钮上显示滚动状态百分比

# Don't modify the following settings unless you know how they work (非必要請不要修改 )
# Choose: readmode,translate,darkmode,hideAside,toc,chat,comment
# Don't repeat 不要重複
rightside_item_order: # 右下角按钮排序及是否隐藏
  enable: false
  hide: # readmode,translate,darkmode,hideAside，这里的按钮需要通过设置按钮展开
  show: # toc,chat,comment，这里的按钮默认出现在右下角
```

### 5. Hexo 项目的管理

在 [建站步骤-项目部署](#Step6. 项目部署 GitHub Pages) 这一步中，我们将 Hexo 生成的静态文件（位于 `./public` 文件夹中）部署到 GitHub Pages 上。为了对 Hexo 项目进行版本管理，我们需要创建一个单独的仓库，这里我们将其命名为 `<username>.github.io.source.hexo`。以下是具体步骤：

Step1. 初始化 Hexo 项目的 Git 仓库

```bash
git init
```

Step2. 移除 Git 缓存中的 butterfly 主题文件夹

```bash
git rm --cached -r themes/butterfly
```

Step3. 将 Butterfly 主题仓库添加为当前 Hexo 项目的子模块

```bash
git submodule add https://github.com/jerryc127/hexo-theme-butterfly.git themes/butterfly
```

Step4. 暂存所有更改并创建一次提交

```bash
git add .  
git commit -m "Remove butterfly theme and add it as a submodule"
```

Step5. 设置远程仓库并推送到 GitHub

```bash
git remote add origin https://github.com/<username>/<username>.github.io.source.hexo.git
git branch -M main     
git push -u origin main 
```

> 注意事项
>
> - 该过程管理的是 Hexo 项目的源代码，而不是生成的静态文件。静态文件的部署是通过 Hexo 的部署命令完成的。
> - 将 Butterfly 主题作为 Hexo 项目的一个子模块，实际上这里 Git 仓库保存的是 Butterfly 主题仓库的一个特定的提交。

### 6. Butterfly - 标签外挂 Tag Plugins

标签外挂是 Hexo 独有的在 Markdown 中增强 UI 的语法，不是标准的 Markdown 格式。

#### 6.1 Note

```yaml
note: # Note (Bootstrap Callout)，可理解为注释块 - 主题配置及用法
  # Part1. 通用设置
  style: flat # note 标签的风格，可选 simple / modern / flat / disabled（禁用所有 note 标签的 css 样式）
  icons: true # note 标签是否显示图标
  border_radius: 3 # note 标签的圆角
  # Offset lighter of background in % for modern and flat styles (modern: -12 | 12; flat: -18 | 6).
  # Offset also applied to label tag variables. This option can work with disabled note tag.
  light_bg_offset: 0
  # 补充说明：icons 和 light_bg_offset 只对方法一生效

  # Part2. 用法一
  # (1) class 【可选】标识，对应 note 标签的不同颜色，可选 default（默认）/ primary / success / info / warning / danger
  # (2) no-icon 【可选】如果有该项，则表示 note 标签不显示图标，可选 no-icon，默认无该项
  # (3) style 【可选】样式，对应 note 标签内的不同风格，可选 simple（默认）/ modern / flat / disabled
  # {% note [class] [no-icon] [style] %}
  # Any content (support inline tags too.io).
  # {% endnote %}

  # Part3. 用法二
  # (1) color 【可选】颜色，可选 default（默认） / blue / pink / red / purple / orange / green
  # (2) icon 【可选】自定义的 icon，支持 font-awesome 图标，也可以配置 no-icon
  # (3) style 【可选】样式，对应 note 标签内的不同风格，可选 simple（默认）/ modern / flat / disabled
  # {% note [color] [icon] [style] %}
  # Any content (support inline tags too.io).
  # {% endnote %}
```

#### 6.2 Gallery Group

```yaml
# GalleryGroup 相册图库 - 用法（无需主题文件中的配置）
  # (1) name 图库名字 (2) 图库描述 (3) 相册地址（点击图片后的跳转地址）(4) 图库封面地址（要显示的图片的地址）
  # <div class="gallery-group-main">
  # {% galleryGroup name description link img-url %}
  # {% galleryGroup name description link img-url %}
  # {% galleryGroup name description link img-url %}
  # </div>
```

#### 6.3 Gallery

```yaml
# Gallery 相册 - 用法（无需主题文件中的配置）
  # 用法一 - 本地
  # (1) lazyload【可选】点击按钮加载更多图片，填写 true / false（默认）。
  # (2) rowHeight【可选】图片显示的高度，如果需要一行显示更多的图片，可设置更小的数字。默认为 220。
  # (3) limit【可选】每次加载多少张照片。默认为 10。
  # {% gallery [lazyload],[rowHeight],[limit] %}
  # markdown 图片格式
  # {% endgallery %}
  # 用法二 - 远程拉取
  # (1) url【必选】识别词，即通过该内容告诉 Butterfly 是远程拉取的方式
  # (2) link【必选】远程的 json 链接，其类型为 Array<{url, alt?, title?}>
  # (3) lazyload【可选】点击按钮加载更多图片，填写 true / false（默认）。
  # (4) rowHeight【可选】图片显示的高度，如果需要一行显示更多的图片，可设置更小的数字。默认为 220。
  # (5) limit【可选】每次加载多少张照片。默认为 10。
  # {% gallery url,[link],[lazyload],[rowHeight],[limit] %}
  # {% endgallery %}
```

#### 6.4 Tag Hide

```yaml
# Tag-Hide 隐藏标签（即将一些内容隐藏起来，提供按钮，允许用户点击显示） - 用法（无需主题文件中的配置）
  # 补充说明：该标签的 content 中不允许有 h1 - h6 等标题，否则会导致渲染异常
  # 用法一 Inline 
  # 补充说明：Inline 用于在文本中添加隐藏内容，因此 content 只限文字，同时不能使用英文逗号，可使用 &sbquo; 代替
  # (1) content【必选】文本内容。
  # (2) display【可选】按钮显示的文字
  # (3) bg【可选】按钮的背景颜色
  # (4) color【可选】按钮文字的颜色
  # {% hideInline content,display,bg,color %}
  # 用法二 Block
  # 补充说明：Block 可以隐藏很多内容，包括图片，代码块等等
  # {% hideBlock display,bg,color %}
  # content
  # {% endhideBlock %}
  # 用法三 Toggle
  # 补充说明 - 1：如果你需要展示的内容太多，可以把它隐藏在收缩框里，需要时再把它展开。
  # 补充说明 - 2：display 不能包含英文逗号，可用 &sbquo; 代替
  # {% hideToggle display,bg,color %}
  # content
  # {% endhideToggle %}
```

#### 6.5 mermaid

```yaml
mermaid: # mermaid，see https://github.com/mermaid-js/mermaid
  # 补充说明：mermaid 标签可以绘制 Flowchart（流程图）、Sequence diagram（时序图 ）、Class Diagram（类别图）、State Diagram（状态图）、Gantt（甘特图）和 Pie Chart（圆形图）
  # 主题配置
  enable: false # 是否启用
  # 内置可选主题: default / forest / dark / neutral
  theme:
    light: default
    dark: dark
  # 用法
  # {% mermaid %}
  # 内容
  # {% endmermaid %}
  # 用法示例
  # {% mermaid %}
  # pie
  #     title Key elements in Product X
  #     "Calcium" : 42.96
  #     "Potassium" : 50.05
  #     "Magnesium" : 10.01
  #     "Iron" :  5
  # {% endmermaid %}
```

#### 6.6 Tabs

```yaml
# Tabs 分页器
  # (1) Unique name 选项卡块标签的唯一名称，不包含逗号。将用于每个选项卡的 #id 作为前缀，后面加上它们的索引号。
  # 如果名称中有空格，在生成 #id 时，所有空格将被替换为连字符。该名称仅需在当前文章/页面的 URL 中保持唯一性。
  # (2) [index] 默认选中的选项卡的索引号。如果未指定，将选择第一个选项卡。如果索引为 -1，则不会选择任何选项卡，
  # 类似于折叠内容的效果。这是一个可选参数。
  # (3) [Tab caption] 当前选项卡的标题。如果未指定标题，则使用唯一名称（Unique name）加上选项卡索引（[index]）作为标题。
  # 如果未指定标题但指定了图标，则标题将为空。
  # (4) [@icons] FontAwesome 图标名称（完整名称，类似于 'fas fa-font'）。可以包含或不包含空格，例如 'Tab caption @icon' 
  # 与 'Tab caption@icon' 是相似的。这是一个可选参数。
  # {% tabs Unique name, [index] %}
  # <!-- tab [Tab caption] [@icon] -->
  # Any content (support inline tags too).
  # <!-- endtab -->
  # {% endtabs %}
```

#### 6.7  Button

```yaml
# Button 按钮
  # (1) [url]：链接；(2) [text]：按钮文字；(3) [icon]：[可选] 图标
  # (4) [color]：[可选] 按钮背景顔色(默认 style 时）或 按钮字体和边框顔色(outline 时)，可选 default / blue / pink / red / purple / orange / green
  # (5) [style]：[可选] 按钮样式 默认实心，可选 outline / 留空
  # (6) [layout]：[可选] 按钮佈局 默认为 line，可选 block / 留空
  # (7) [position]：[可选] 按钮位置 前提是设置了 layout 为 block 默认为左边，可选 center / right / 留空
  # (8) [size]：[可选] 按钮大小，可选 larger / 留空
  # {% btn [url],[text],[icon],[color] [style] [layout] [position] [size] %
```

#### 6.8 InlineImg

```yaml
# inlineImg 内联图片
  # 补充说明：主题图片默认以'块级元素'显示，通过内联图片可以将图片以'内联元素'显示
  # [src]：图片链接
  # [height]：【可选】图片高度限制
  # {% inlineImg [src] [height] %}
```

#### 6.9 Label

```yaml
# label 标签
  # 补充说明：label 用于给段落文字上样式，同时注意，不要在段落开头使用 label 标签
  # (1) text 文字
  # (2) color【可选】背景颜色，可选 default（默认值） / blue / pink / red / purple / orange / green
  # {% label text color %}
```

#### 6.10 Timeline

```yaml
# timeline 时间线
  # (1) title 标题（时间线或时间线中某个节点的标题）
  # (2) color 颜色（时间线的颜色），可选 default（默认）/ blue / pink / red / purple / orange / green
  # {% timeline title,color %}
  # <!-- timeline title -->
  # xxxxx
  # <!-- endtimeline -->
  # <!-- timeline title -->
  # xxxxx
  # <!-- endtimeline -->
  # {% endtimeline %}
```

#### 6.11 Flink

```yaml
# flink 友情链接效果
  # {% flink %}
  # - class_name: # 类名
  #   class_desc: # 类描述
  #   link_list: # 类链接列表
  #     - name: # 链接名
  #       link: # 链接
  #       avatar: # 链接头像
  #       descr: # 链接描述
  #     - xxx
  # - xxx
  # {% endflink %}
```

#### 6.12 abcjs

```yaml
abcjs: # 乐谱渲染，See https://github.com/paulrosen/abcjs
  # 主题配置
  enable: true
  per_page: true
  # 用法
  # {% score %}
  # 乐谱代码
  # {% endscore %}
```

#### 6.13 series

```yaml
series: # 系列文章
  # 主题配置
  enable: true # 是否启用
  orderBy: "title" # 排序依据，可选 title / data
  order: 1 # 排序，可选 1（升序） / -1（降序） 
  number: true
  # 用法
  # {% series %}
  # {% series [series name] %}
  # 补充说明：series 是文章的一个标识，可以通过 front-matter 的 series 字段给文章添加标识
  # 如果使用 series 标签插件，则会把相同标识的文章以列表的形式展示；
  # 如果使用 series 标签外挂，但是不写 series 标识，则默认使用该标签插件所在的文章的 series 标识（即 front-matter 中的配置）
```

### 7. Butterfly - 主题配置 2

#### 7.1 数学公式设置

```yaml
# 补充说明 1：如果这里设置 mathjax 或 katex 为 true，则每一个页面都会加载 mathjax 或 katex 对应的 js 代码；
# 如果为 false，则只有在每一页的 front-matter 中设置 mathjax 或 katex 为 true 时，该页面才会加载对应的 js 代码
# 补充说明 2：不要在标题中使用 mathjax 或 katex 语法
# 补充说明 3：MathJax 和 KaTeX 都是用于在网页上渲染数学公式的 JavaScript 库，后者体积更小，渲染更快；建议使用 katex 语法
mathjax: # MathJax
  enable: false # 是否启用
  per_page: false # true（每一页都加载 mathjax.js）/ false（需要时加载，即在文章的 front-matter 设置 mathjax: true）
  # 补充说明：为了使用 MathJax 渲染，需要通过以下步骤
  # Step1. 卸载 marked 渲染引擎，下载 kramed 渲染引擎（用于支持 mathjax 渲染）
  # npm uninstall hexo-renderer-marked --save
  # npm install hexo-renderer-kramed --save
  # Step2. 修改 Hexo 的配置文件 _config.yml
  # kramed:
  #   gfm: true
  #   pedantic: false
  #   sanitize: false
  #   tables: true
  #   breaks: true
  #   smartLists: true
  #   smartypants: true

katex: # KaTeX
  enable: true # 是否启用
  per_page: false # true（每一页都加载 katex.js）/ false（需要时加载，即在文章的 front-matter 设置 katex: true）
  hide_scrollbar: true
  # 补充说明：为了使用 KaTex 渲染，需要通过以下步骤
  # Step1. 禁用 MathJax，启用 KaTex
  # Step2. 卸载 marked 渲染引擎及可能潜在的 kramed 渲染引擎，下载 markdown-it 渲染插件
  # npm un hexo-renderer-marked --save # 如果有安装这个的话，卸载
  # npm un hexo-renderer-kramed --save # 如果有安装这个的话，卸载
  # npm i hexo-renderer-markdown-it --save # 需要安装这个渲染插件
  # npm install katex @renbaoshuo/markdown-it-katex #需要安装这个 katex 插件
  # Step3. 修改 Hexo 的配置文件 _config.yml
  # markdown:
  #   plugins:
  #     - '@renbaoshuo/markdown-it-katex'
```

#### 7.2 搜索设置

```yaml
# see https://butterfly.js.org/posts/ceeb73f/#搜索系統
algolia_search: # Algolia search
  enable: false
  hits:
    per_page: 6

local_search: # Local search
  enable: false
  # Preload the search data when the page loads.
  preload: false
  # Show top n results per article, show all results by setting to -1
  top_n_per_article: 1
  # Unescape html strings to the readable one.
  unescape: false
  CDN:

docsearch: # Docsearch，当博客搭建完毕后，预期使用该技术进行内容检索
  enable: false
  appId:
  apiKey:
  indexName:
  option:
```

#### 7.3 分享设置

```yaml
# 补充说明：下边的两个分享服务商，同时只能是使用一个
sharejs: # Share.js，see https://github.com/overtrue/share.js
  enable: true
  sites: twitter,wechat,qq,weibo # facebook,twitter,wechat,weibo,qq

addtoany: # AddToAny，https://www.addtoany.com/
  enable: false
  item: facebook,twitter,wechat,sina_weibo,facebook_messenger,email,copy_link
```

#### 7.4 评论设置

```yaml
comments:
  use: Utterances # 可选 Disqus / Disqusjs / Livere / Gitalk / Valine / Waline / Utterances / Facebook Comments / Twikoo / Giscus / Remark42 / Artalk / Valine / Disqus
  # 补充说明 - 1：只有在 comments.use 中填写服务商的名字，才算做开启了评论功能
  # 补充说明 - 2：comments.use 中可以最多填写两家评论服务商，默认使用第一个
  # 补充说明 - 3：不能同时使用 Disqus 和 Disqusjs，会出错
  text: true # 是否显示评论服务商的名字
  lazyload: false # 是否为评论开启懒加载，开启后 (1) 只有滚动到评论位置时才会加载评论所需的资源 (2) 评论数将不再显示
  count: false # 是否在文章顶部显示评论数，其中 Livere / Giscus / Utterances 不支持评论数的显示
  card_post_count: false # 是否在首页文章卡片显示评论数，其中 Gitalk / Livere / Giscus / Utterances 不支持评论数的显示

utterances:
  enable: true
  repo: Nasir1423/blog-comment # 填写你的 GitHub 仓库
  issue_term: pathname # 根据页面 URL 生成 Issue，Issue Mapping: pathname/url/title/og:title
  theme: github-light # 评论区主题，可以设置为 github-light, github-dark, preferred-color-scheme 等
  light_theme: github-light # 评论区日间主题
  dark_theme: photon-dark # 评论区夜间主题
  # 主题可选：github-light/github-dark/github-dark-orange/icy-dark/dark-blue/photon-dark
  label: "" # 自定义标签，默认留空
  crossorigin: anonymous # 跨域配置

# disqus
# https://disqus.com/
disqus:
  shortname:
  apikey: # For newest comments widget

# Alternative Disqus - Render comments with Disqus API
# DisqusJS 評論系統，可以實現在網路審查地區載入 Disqus 評論列表，兼容原版
# https://github.com/SukkaW/DisqusJS
disqusjs:
  shortname:
  apikey:
  option:

# livere (來必力)
# https://www.livere.com/
livere:
  uid:

# gitalk
# https://github.com/gitalk/gitalk
gitalk:
  client_id:
  client_secret:
  repo:
  owner:
  admin:
  option:

# valine
# https://valine.js.org
valine:
  appId: # leancloud application app id
  appKey: # leancloud application app key
  avatar: monsterid # gravatar style https://valine.js.org/#/avatar
  serverURLs: # This configuration is suitable for domestic custom domain name users, overseas version will be automatically detected (no need to manually fill in)
  bg: # valine background
  visitor: false
  option:

# waline - A simple comment system with backend support fork from Valine
# https://waline.js.org/
waline:
  serverURL: # Waline server address url
  bg: # waline background
  pageview: false
  option:

# Facebook Comments Plugin
# https://developers.facebook.com/docs/plugins/comments/
facebook_comments:
  app_id:
  user_id: # optional
  pageSize: 10 # The number of comments to show
  order_by: social # social/time/reverse_time
  lang: zh_TW # Language en_US/zh_CN/zh_TW and so on

# Twikoo
# https://github.com/imaegoo/twikoo
twikoo:
  envId:
  region:
  visitor: false
  option:

# Giscus
# https://giscus.app/
giscus:
  repo:
  repo_id:
  category_id:
  theme:
    light: light
    dark: dark
  option:

# Remark42
# https://remark42.com/docs/configuration/frontend/
remark42:
  host: # Your Host URL
  siteId: # Your Site ID
  option:

# Artalk
# https://artalk.js.org/guide/frontend/config.html
artalk:
  server:
  site:
  visitor: false
  option:
```

#### 7.5 在线聊天设置

```yaml
# 这里不采用这个功能，考虑到博客的不必要性，因此这里仅使用默认功能

# Chat Button [recommend]
# It will create a button in the bottom right corner of website, and hide the origin button
chat_btn: false

# The origin chat button is displayed when scrolling up, and the button is hidden when scrolling down
chat_hide_show: false

# chatra
# https://chatra.io/
chatra:
  enable: false
  id:

# tidio
# https://www.tidio.com/
tidio:
  enable: false
  public_key:

# daovoice
# http://dashboard.daovoice.io/app
daovoice:
  enable: false
  app_id:

# crisp
# https://crisp.chat/en/
crisp:
  enable: false
  website_id:

# messenger
# https://developers.facebook.com/docs/messenger-platform/discovery/facebook-chat-plugin/
messenger:
  enable: false
  pageID:
  lang: zh_TW # Language en_US/zh_CN/zh_TW and so on
```

#### 7.6 统计设置

```yaml
# Baidu Analytics
# https://tongji.baidu.com/web/welcome/login
baidu_analytics:

# Google Analytics
# https://analytics.google.com/analytics/web/
google_analytics: G-JRLJPHP21V

# Cloudflare Analytics
# https://www.cloudflare.com/zh-tw/web-analytics/
cloudflare_analytics:

# Microsoft Clarity
# https://clarity.microsoft.com/
microsoft_clarity:
```

#### 7.7 广告设置

```yaml
# Google Adsense (谷歌廣告)
google_adsense:
  enable: false
  auto_ads: true
  js: https://pagead2.googlesyndication.com/pagead/js/adsbygoogle.js
  client:
  enable_page_level_ads: true

# Insert ads manually (手動插入廣告)
# ad:
#   index:
#   aside:
#   post:
```

#### 7.8 网站验证设置

```yaml
# “网站验证”指的是向搜索引擎证明你对网站的所有权或管理权限。
# 通常，如果你希望搜索引擎（如 Google、Bing 等）能够收录并索引你的网站内容，
# 首先需要在相应的搜索引擎管理平台上提交你的网站并进行验证。
# 补充说明：由于这里使用了 DNS 验证，因此不做配置（即使用 HTML 验证）
site_verification:
  # - name: google-site-verification
  #   content: xxxxxx
  # - name: baidu-site-verification
  #   content: xxxxxxx
```

这里以**谷歌**为例，讲述如何让你的网站被谷歌收录，从而可以通过谷歌搜索引擎检索到你的网站的文章。

1. 登录 [Search Console](https://search.google.com/search-console?hl=zh-CN)，登录后提交你的网站地址并进行所有权验证

2. 生成站点地图 Site Map，用于描述你的网站结构，便于搜索引擎快速爬取

   - 安装 Site Map 生成插件

     ```bash
     npm install hexo-generator-sitemap --save
     ```

   - 配置 Hexo 项目的配置文件 `_config.yml`

     ```yaml
     sitemap:
     	path: sitemap.xml
     ```

   - 重新部署 Hexo 项目

     ```bash
     hexo clean
     hexo generate
     hexo deploy
     ```

     > 此时可以在 `https://xxxx.github.io/sitemap.xml` 查看到生成的 Site Map 了

3. 在 [Search Console](https://search.google.com/search-console?hl=zh-CN) 中配置站点地图

4. 谷歌搜索 `site:https://xxxx.github.io` 检查你的网站是否已经被收录

#### 7.9 美化设置

```yaml
# theme_color: # 主题色
# Theme color for customize
# Notice: color value must in double quotes like "#000" or may cause error!
# enable: true
# main: "#49B1F5"
# paginator: "#00c4b6"
# button_hover: "#FF7242"
# text_selection: "#00c4b6"
# link_color: "#99a9bf"
# meta_color: "#858585"
# hr_color: "#A4D8FA"
# code_foreground: "#F47466"
# code_background: "rgba(27, 31, 35, .05)"
# toc_color: "#00c4b6"
# blockquote_padding_color: "#49b1f5"
# blockquote_background_color: "#49b1f5"
# scrollbar_color: "#49b1f5"
# meta_theme_color_light: "ffffff"
# meta_theme_color_dark: "#0d0d0d"

# region 主页顶部图
index_site_info_top: # 主页标题距离顶部的距离，可选 300px / 300em / 300rem / 10%（默认标题在中间）
index_top_img_height: # 主页顶部图（top_img）的高度，可选 300px / 300em / 300rem（不可使用百分比）（默认顶部图全屏）
# endregion

text_align_justify: false # 使文字向两侧对齐（即拉伸每一行，使得每行等宽），对最后一行无效

background: # 网站背景，可选颜色值 [HEX / RGB / 颜色单词 / 渐变色] or 图片 [url(http://xxxxxx.com/xxx.jpg)]

footer_bg: false # 网站底部背景，可选 (1) 留空 / false：显示默认颜色 (2) img 链接：显示图片 (3) 颜色值，如 HEX / RGB / 颜色单词 / 渐变色：显示对应的颜色 (4) true：与顶部图一样

activate_power_mode: # Typewriter Effect (打字效果)，see https://github.com/disjukr/activate-power-mode
  enable: false
  colorful: true # open particle animation (冒光特效)
  shake: true #  open shake (抖動特效)
  mobile: false

# region 背景特效
canvas_ribbon: # canvas_ribbon (靜止彩帶背景)，See: https://github.com/hustcc/ribbon.js
  # 好看的綵帶背景，可設置每次刷新更換綵帶，或者每次點擊更換綵帶
  enable: false
  size: 150
  alpha: 0.6
  zIndex: -1
  click_to_change: false # 设置是否每次点击都更换綵带
  mobile: false # false 手机端不显示；true 手机端显示

canvas_fluttering_ribbon: # Fluttering Ribbon (动态彩带背景)
  # 好看的綵带背景，会飘动
  enable: false
  mobile: false # false 手机端不显示 true 手机端显示

canvas_nest: # canvas_nest (跟踪鼠标的动态彩带背景)，see https://github.com/hustcc/canvas-nest.js
  enable: false
  color: "0,0,255" #color of lines, default: '0,0,0'; RGB values: (R,G,B).(note: use ',' to separate.)
  opacity: 0.7 # the opacity of line (0~1), default: 0.5.
  zIndex: -1 # z-index property of the background, default: -1.
  count: 99 # the number of lines, default: 99.
  mobile: false
# endregion

# region 鼠标点击效果
fireworks: # Mouse click effects: fireworks (鼠标点击效果：烟火特效)
  enable: false
  zIndex: 9999 # -1 or 9999，zIndex 建议只在 -1 和 9999 上选，-1 代表烟火效果在底部，9999 代表烟火效果在前面
  mobile: false

click_heart: # Mouse click effects: Heart symbol (鼠标点击效果: 爱心)
  enable: false
  mobile: false

clickShowText: # Mouse click effects: words (鼠标点击效果: 文字)
  enable: true
  text:
    # - I
    # - LOVE
    # - YOU
    - Prosperity
    - Democracy
    - Civility
    - Harmony
    - Freedom
    - Equality
    - Justice
    - Rule of Law
    - Patriotism
    - Dedication
    - Integrity
    - Friendliness
  fontSize: 15px
  random: true # 文字随机显示
  mobile: false
# endregion

beautify: # Beautify (页面美化)
  # 页面美化会修改 oi, li, h1-h5 的样式
  enable: false
  field: post # site（全站生效） / post（仅文章页生效）
  title-prefix-icon: # '\f0c1'，font awesome 的 icon 的 unicode 数
  title-prefix-icon-color: # '#F47466'

# region 自定义字体和字体大小
font: # 全局字体修改，非必要不修改该配置
  global-font-size:
  code-font-size:
  font-family:
  code-font-family:

blog_title_font: # Blog 标题字体（包括标题和子标题）
  font_link: # 网络字体
  font-family:
# endregion

subtitle: # 网站主页副标题
  enable: true # 是否启用
  # Typewriter Effect (打字效果)
  effect: true
  startDelay: 300 # time before typing starts in milliseconds
  typeSpeed: 150 # type speed in milliseconds
  backSpeed: 50 # backspacing speed in milliseconds
  # loop (循环打字)
  loop: true
  # source 調用第三方服務
  # source: false 關閉調用
  # source: 1  調用一言網的一句話（簡體） https://hitokoto.cn/
  # source: 2  調用一句網（簡體） http://yijuzhan.com/
  # source: 3  調用今日詩詞（簡體） https://www.jinrishici.com/
  # subtitle 會先顯示 source , 再顯示 sub 的內容
  source: false
  # 如果關閉打字效果，subtitle 只會顯示 sub 的第一行文字
  sub:
    - 弓，其实是我最不擅长的武器。正因如此，我才要征服它。
    - I am the least adept with a bow. And that is precisely why I must master it.

preloader: # Loading Animation (页面加载动画)
  enable: true
  # source
  # 1. fullpage-loading
  # 2. pace (progress bar)
  source: 2
  # pace theme (see https://codebyzach.github.io/pace/)
  pace_css_url: /styles/minimal.css
```

#### 7.10 字数统计设置

```yaml
wordcount: # see see https://butterfly.js.org/posts/ceeb73f/#字數統計
  # 补充说明：为了确保该功能的实现，需要安装相关包
  # npm install hexo-wordcount --save
  enable: true # 是否启用字数统计
  post_wordcount: true # 是否启用单篇文章的字数统计
  min2read: true # 是否启用阅读时间的估算
  total_wordcount: true # 是否启用站点所有文章的总字数统计
```

#### 7.11 图片大图查看设置

```yaml
# 补充说明：以下两种模式最多只能选择一种
medium_zoom: false # medium-zoom，https://github.com/francoischalifour/medium-zoom
fancybox: true # fancybox，https://fancyapps.com/fancybox/
```

#### 7.12 Pjax 设置

```yaml
pjax:
  # It may contain bugs and unstable, give feedback when you find the bugs.
  # https://github.com/MoOx/pjax
  # 关于 Pjax
  # 1. 概述：Pjax (PushState + AJAX) 是一种结合了 AJAX 和 HTML5 history.pushState() API 的技术，
  # 用来优化网页的部分内容加载，提高页面切换时的响应速度。
  # 2. Pjax 的工作原理：Pjax 的核心思想是通过 AJAX 来加载网页的部分内容，而不是重新加载整个页面。
  # 它利用 HTML5 history.pushState() API 来管理浏览器的 URL 和历史记录。
  # 具体过程为 (1) 拦截链接点击和表单提交 (2) 通过 AJAX 异步请求新页面 (3) 动态更新内容
  # (4) 更新浏览器的 URL (5) 触发事件和页面生命周期钩子
  # 3. Pjax 的优势：(1) 减少不必要的加载 (2) 提升用户体验 (3) 保留浏览器原生功能 (4) 减少服务器负担
  # Butterfly 中的 Pjax 配置
  # 当用户点击链接，通过 ajax 更新页面需要变化的部分，然后使用 HTML5 的 pushState 修改浏览器的 URL 地址。
  # 这样可以不用重复加载相同的资源（css / js）， 从而提升网页的加载速度。
  enable: false # 是否启用，Butterfly 的 Pjax 目前仍有一些问题，故不推荐使用
  exclude: # 用于指定哪些网页不适用 Pjax 技术，即点击该网页会重新加载网站
    # - xxxx
    # - xxxx
```

#### 7.13 弹窗设置

```yaml
snackbar:
  # https://github.com/polonel/SnackBar
  enable: false
  position: bottom-left # 弹窗位置，可选 top-left / top-center / top-right / bottom-left / bottom-center / bottom-right
  bg_light: "#49b1f5" # The background color of Toast Notification in light mode
  bg_dark: "#1f1f1f" # The background color of Toast Notification in dark mode
```

#### 7.14 预加载设置

```yaml
# https://instant.page/
instantpage: false
# 当鼠标悬停到链接上超过 65 毫秒时，Instantpage 会对该链接进行预加载，可以提升访问速度。
```

#### 7.15 中英文之间添加空格设置

```yaml
# Insert a space between Chinese character and English character (中英文之間添加空格)
pangu:
  # https://github.com/vinta/pangu.js
  enable: true
  field: site # site / post，post(只在文章页生效)和site(全站生效)
```

#### 7.16 PWA 设置

```yaml
# 1. 概述：PWA（渐进式网页应用）可以简单理解为一种介于手机网页和手机APP之间的应用。
# 2. 如何为 Butterfly 添加 PWA 特性？
# region PWA 配置步骤
# (1) 根目录执行 => npm install hexo-offline --save
# (2) 根目录创建 => hexo-offline.config.cjs，内容为
# // offline config passed to workbox-build.
# module.exports = {
#   globPatterns: ['**/*.{js,html,css,png,jpg,gif,svg,webp,eot,ttf,woff,woff2}'],
#   // 静态文件合集，如果你的站点使用了例如 webp 格式的文件，请将文件类型添加进去。
#   globDirectory: 'public',
#   swDest: 'public/service-worker.js',
#   maximumFileSizeToCacheInBytes: 10485760, // 缓存的最大文件大小，以字节为单位。
#   skipWaiting: true,
#   clientsClaim: true,
#   runtimeCaching: [ // 如果你需要加载 CDN 资源，请配置该选项，如果没有，可以不配置。
#     // CDNs - should be CacheFirst, since they should be used specific versions so should not change
#     {
#       urlPattern: /^https:\/\/cdn\.example\.com\/.*/, // 可替换成你的 URL
#       handler: 'CacheFirst'
#     }
#   ]
# }
# (3) 在主题配置文件 _config.butterfly.yml or themes/butterfly/_config.yml 中开启 pwa 选项，如下
# (4) 在 source/ 目录中创建 manifest.json 文件，内容为
# {
#     "name": "string",
#     "short_name": "Junzhou",
#     "theme_color": "#49b1f5",
#     "background_color": "#49b1f5",
#     "display": "standalone",
#     "scope": "/",
#     "start_url": "/",
#     "icons": [
#         {
#           "src": "images/pwaicons/36.png",
#           "sizes": "36x36",
#           "type": "image/png"
#         },
#         {
#             "src": "images/pwaicons/48.png",
#           "sizes": "48x48",
#           "type": "image/png"
#         },
#         {
#           "src": "images/pwaicons/72.png",
#           "sizes": "72x72",
#           "type": "image/png"
#         },
#         {
#           "src": "images/pwaicons/96.png",
#           "sizes": "96x96",
#           "type": "image/png"
#         },
#         {
#           "src": "images/pwaicons/144.png",
#           "sizes": "144x144",
#           "type": "image/png"
#         },
#         {
#           "src": "images/pwaicons/192.png",
#           "sizes": "192x192",
#           "type": "image/png"
#         },
#         {
#             "src": "images/pwaicons/512.png",
#             "sizes": "512x512",
#             "type": "image/png"
#           }
#       ],
#       "splash_pages": null
#   }
# (5) 可以通过Chrome插件Lighthouse检查 PWA 配置是否生效以及配置是否正确。
# endregion
# pwa:
# See https://github.com/JLHwung/hexo-offline
# enable: false
# manifest: /pwa/manifest.json
# apple_touch_icon: /pwa/apple-touch-icon.png
# favicon_32_32: /pwa/32.png
# favicon_16_16: /pwa/16.png
# mask_icon: /pwa/safari-pinned-tab.svg
```

#### 7.17 元标签设置

```yaml
Open_Graph_meta:
  # https://developers.facebook.com/docs/sharing/webmasters/
  enable: true # 是否启用 Open Graph 元标签功能
  option: # 可选配置项的列表，包含了不同社交平台相关的元标签选项。
    # twitter 相关配置
    # twitter_card:
    # twitter_image:
    # twitter_id:
    # twitter_site:
    # google 相关配置
    # google_plus: # 该配置已废弃
    # facebook 相关配置
    # fb_admins:
    # fb_app_id:
```

#### 7.18 CSS 前缀设置

```yaml
css_prefix: true # 是否为一些 CSS 添加前缀（为了确保样式生效），该选项会添加 20% 的体积
```

#### 7.19 代码注入设置

```yaml
inject:
  # 插入代码到头部 </head> 之前 和 底部 </body> 之前
  # 该配置允许以标准的 HTML 格式添加内容，支持添加 js / css / meta 等等内容
  # 补充：注意网站根目录问题，即如果你的网站根目录不是 '/'，使用本地图片时，需加上你的根目录。
  head:
    # - <link rel="stylesheet" href="/xxx.css">
  bottom:
    # - <script src="xxxx"></script>
```

#### 7.20 CDN 设置

```yaml
# Don't modify the following settings unless you know how they work
# 非必要請不要修改
CDN:
  # The CDN provider of internal scripts (主題內部 js 的 cdn 配置)
  # option: local（本地加载）/ jsdelivr / unpkg / cdnjs / custom（自定义格式，需配置 CDN.custom_format）
  # Dev version can only choose local. ( dev 版的主題只能設置為 local )
  internal_provider: local

  # The CDN provider of third party scripts (第三方 js 的 cdn 配置)
  # option: local（本地加载）/ jsdelivr / unpkg / cdnjs / custom（自定义格式，需配置 CDN.custom_format）
  # when set it to local, you need to install hexo-butterfly-extjs
  third_party_provider: jsdelivr

  # Add version number to url, true or false（上是否为 cdn 加上指定版本号）
  version: true

  # Custom format
  # For example: https://cdn.staticfile.org/${cdnjs_name}/${version}/${min_cdnjs_file}
  # 参数 解释
  # name npm 上的包名
  # file npm 上的文件路径
  # min_file npm 上的文件路径（压缩过的文件）
  # cdnjs_name cdnjs 上的包名
  # cdnjs_file cdnjs 上的文件路径
  # min_cdnjs_file cdnjs 上的文件路径（压缩过的文件）
  # version 插件版本号
  custom_format:

  option: # 自定义 CDN，覆盖原有配置
    # abcjs_basic_js:
    # activate_power_mode:
    # algolia_js:
    # algolia_search:
    # aplayer_css:
    # aplayer_js:
    # artalk_css:
    # artalk_js:
    # blueimp_md5:
    # busuanzi: https://cdn.jsdelivr.net/npm/busuanzi@2.3.0/bsz.pure.mini.js
    # canvas_fluttering_ribbon:
    # canvas_nest:
    # canvas_ribbon:
    # click_heart:
    # clickShowText:
    # disqusjs:
    # disqusjs_css:
    # docsearch_css:
    # docsearch_js:
    # egjs_infinitegrid:
    # fancybox:
    # fancybox_css:
    # fireworks:
    # fontawesome:
    # gitalk:
    # gitalk_css:
    # giscus:
    # instantpage:
    # instantsearch:
    # katex:
    # katex_copytex:
    # lazyload:
    # local_search:
    # main:
    # main_css:
    # mathjax:
    # medium_zoom:
    # mermaid:
    # meting_js:
    # pangu:
    # prismjs_autoloader:
    # prismjs_js:
    # prismjs_lineNumber_js:
    # pjax:
    # sharejs:
    # sharejs_css:
    # snackbar:
    # snackbar_css:
    # translate:
    # twikoo:
    # typed:
    # utils:
    # valine:
    # waline_css:
    # waline_js:
```

#### 7.21 图片懒加载设置

```yaml
# https://github.com/verlok/vanilla-lazyload
lazyload:
  enable: false
  field: site # site / post
  placeholder:
  blur: false
```

#### 7.22 分类标签页的 UI 设置

```yaml
# index - same as Homepage UI (index 值代表 UI 將與首頁的 UI 一樣)
# default - same as archives UI 默認跟 archives 頁面 UI 一樣
category_ui: # 留空或 index
tag_ui: # 留空或 index
```

#### 7.23 header、footer 的蒙版效果设置

```yaml
mask:
  header: true
  footer: true
```

#### 7.24 右小角按钮位置设置

```yaml
rightside_bottom:
```

#### 7.25 网页进入效果设置

```yaml
enter_transitions: true
```

#### 7.26 水平分割线图标设置

```yaml
hr_icon:
  enable: true
  icon: # the unicode value of Font Awesome icon, such as '\3423'
  icon-top:
```

#### 7.27 网页默认显示设置

```yaml
display_mode: light # light (default) / dark
```

#### 7.28 aplyer 设置

```yaml
# 控制 Hexo Butterfly 主题中的 APlayer 播放器注入设置
aplayerInject:
  enable: false
  per_page: true
```
