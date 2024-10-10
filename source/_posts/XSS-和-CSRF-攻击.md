---
title: XSS 和 CSRF 攻击
date: 2024-09-25 14:38:15
tags: 网络安全
categories:
  - 前端面试
  - 八股文
description: XSS 和 CSRF 攻击的介绍、分类、防御方式，以及对这两种网络攻击方式的对比。存在疑问？在评论区留言吧！
---

# 一、XSS

## 1. 概述

XSS（Cross Site Script）**跨站脚本攻击**，指的是**攻击者**向网站**嵌入恶意脚本**，使得用户在**浏览该页面时执行这些脚本**，从而达到**窃取用户数据**（如 cookie）的目的。

## 2. 分类

XSS 攻击可分为三种：**存储型**（持久型）、**反射型**（非持久型）、**基于 DOM**。

### 2.1 存储型

1. 概述：**存储型 XSS**，也称为**持久型 XSS**，指的是：① 攻击者将恶意脚本提交到网站**服务器**的数据库中；② 当用户通过浏览器请求包含该恶意脚本的页面时；③ 恶意脚本会被执行，并将用户的 cookie 等敏感信息上传到攻击者的服务器。
2. 示例：2015 年，喜马拉雅出现存储型 XSS 漏洞。黑客将恶意 JavaScript 代码作为专辑名称提交，因服务器未严格过滤，这段代码被存储在数据库中。当其他用户访问该专辑时，恶意脚本执行，窃取用户的 Cookie 信息，并上传到黑客的服务器。黑客因此可以非法访问用户账号。

### 2.2 反射型

1. 概述：**反射型 XSS**，也称为**非持久型 XSS**，指的是：① 攻击者**诱导**用户点击一个恶意链接、提交表单或访问恶意网站；② 用户实际发送了一段**包含恶意脚本的请求**（即 **XSS 代码出现在请求 URL 中**）给网页服务器；③ 服务器解析请求并响应，响应内容中包含注入的恶意脚本；④ 浏览器在解析服务器响应时执行了恶意脚本，从而导致用户的 cookie 等敏感信息被窃取。

2. 示例：假设服务端的路由和视图如下，

   ```js
   var express = require('express');
   var router = express.Router();
    
    
   /* GET home page. */
   router.get('/', function(req, res, next) {
     res.render('index', { title: 'Express',xss:req.query.xss });
   });
    
    
   module.exports = router;
   ```

   ```ejs
   <!DOCTYPE html>
   <!-- index.ejs -->
   <!-- 该视图将 URL 中的 xss 参数显示在页面 -->
   <html>
       <head>
         <title><%= title %></title>
         <link rel='stylesheet' href='/stylesheets/style.css' />
       </head>
       <body>
         <h1><%= title %></h1>
         <p>Welcome to <%= title %></p>
         <div>
             <%- xss %>
         </div>
       </body>
   </html>
   ```

   当用户访问 `http://localhost:3000/?xss=123` 时，页面正常显示，但当用户访问 `http://localhost:3000/?xss=alert('你被xss攻击了')` 时，页面会跳出一个弹窗，即恶意脚本被执行。

### 2.3 基于 DOM

1. 概述：**基于 DOM 的 XSS 攻击**，指的是：① 攻击者通过各种手段（如网络劫持、在传输过程中修改 HTML 页面内容或诱导用户点击恶意链接等）**将恶意脚本注入**用户访问的页面中；② 这些恶意脚本在浏览器中执行，窃取用户的敏感信息。

2. 示例：当用户访问以下链接，

   ```txt
   http://example.com/?name=<script>alert('XSS攻击');</script>
   ```

   如果网页的 JavaScript 直接将 `name` 参数插入到页面中而未进行过滤，恶意脚本会被执行，触发警报，显示“XSS攻击”，从而窃取用户的敏感信息。

## 3. 防御

1. 根据恶意脚本**是否要经过网页服务器处理**，可以进一步将 XSS 攻击分为以下两种

   - **服务端安全漏洞**：存储型 XSS 攻击、反射型 XSS 攻击

   - **前端的安全漏洞**：基于 DOM 的 XSS 攻击

2. XSS 攻击的共性：① 向浏览器中**嵌入**恶意脚本 ② 再通过恶意脚本**窃取**用户信息发送给攻击者部署的恶意服务器上

### 3.1 服务端：用户输入 - 编码、解码和过滤

> 适用于存储型 & 反射型 XSS 攻击

1. **编码**：即将用户输入中的**特殊字符**（如 `<`、`>` 等）进行字符实体编码。

   ```js
   // 用户输入
   code: <script>alert('你被 xss 攻击了')</script> 
   // 用户输入的过滤结果
   code: &lt;script&gt;alert(&#39; 你被 xss 攻击了 &#39;)&lt;/script&gt;
   ```

2. **解码**：为了确保某些内容可以按原样显示，需要对用户编码的内容进行解码。

3. **过滤**：即将用户输入中的**不合法的内容**（如 script、iframe 节点等）过滤掉。

   ```js
   // 用户输入
   code: <script>alert('你被 xss 攻击了')</script> 
   // 用户输入的过滤结果
   code: 
   ```

### 3.2 前端：内容安全策略（CSP）

> 适用于所有 XSS 攻击；这里对于 CSP 的介绍有些详细，可以只看[概念](#概念)、[实现](#实现)和[用例](#用例)

#### 概念

CSP（Content Security Policy）**内容安全策略**，指的是一个额外的安全层，用于**检测并削弱**某些特定类型的攻击，包括**跨站脚本攻击**（XSS 攻击）和**数据注入攻击**等。通过 CSP 你可以为浏览器配置**一组安全策略**，如 ① 指定**有效域**，即浏览器可以执行哪些来源的可执行脚本；② 指定**有效资源**，即浏览器可以加载哪些资源；等等。

> 兼容性：浏览器对 CSP 是**向后兼容**的，即：不支持 CSP 的浏览器会**忽略** CSP 策略，而使用**标准同源策略**；对于支持 CSP 的浏览器，如果网页没有指定 CSP 策略，则也会使用**标准的同源策略**。

#### 实现

CSP 可以 ① 通过配置**服务器**返回的 `Content-Security-Policy` HTTP 标头；② 通过 `<meta>` 元素来进行配置并启用。

- `Content-Security-Policy` HTTP 标头的适用语法为：`Content-Security-Policy: policy`

- `<meta>` 元素的使用语法为：`<meta http-equiv="Content-Security-Policy" content=policy />`

> `policy` 参数是一个表示 **CSP 策略**的**字符串**，其包含**一组 CSP 策略指令**。

> 注-1：CSP 的某些功能（如发送 CSP 违规报告）**仅在使用 HTTP 标头时可用**。
>
> 注-2：`X-Content-Security-Policy` 是旧版本的用于配置 CSP 策略的 HTTP 标头。

#### 策略指令

CSP 策略由一系列策略指令所组成，每个策略指令都描述了**针对某个特定资源的类型以及生效的范围**。常见的策略指令为，

|   策略指令    |                             含义                             |
| :-----------: | :----------------------------------------------------------: |
| `default-src` |            **备选**的源策略，适用于所有资源类型。            |
| `script-src`  | 允许执行的 **JavaScript 脚本**的源策略。<br />支持 `<script>` 这种通过 URL 加载的脚本，也支持通过 `onclick` 事件触发的**内联脚本**。 |
|   `img-src`   | 允许加载的**图片**的源策略。<br />这里的所说的图片也包括**网站图标** `favicon`。 |
| `connect-src` | 允许**使用脚本请求**的源策略。<br />这里的使用脚本请求的方式涵盖 `WebSocket`、`<a>`、`fetch`、`XMLHttpRequest` 等 |
|  `frame-src`  |               允许嵌套的 `<iframe>` 的源策略。               |
|  `style-src`  |                允许加载的**样式表**的源策略。                |
| `object-src`  |                允许加载的 `<object>` 的源策略                |

每个策略指令允许指定**一个或多个源**，格式为 `directive: <source>[ <source>]`

常见的源的可选值为，

|       源值        |                             含义                             |
| :---------------: | :----------------------------------------------------------: |
|  `<host-source>`  | **站点地址**，由主机名（域名或 IP 地址） + 可选的协议名 + 可选的端口号组成，如 `https://store.example.com`。 |
| `<scheme-source>` | **协议名**，可选 `'http:'`  或者  `'https:'` 等。**必须带有冒号，不要有单引号**。 |
|     `'self'`      | **当前站点对应的源**。这意味着，任何请求都必须发送到与当前站点相同的 URL（必须协议、域名、端口号都相同）。**该取值必须有单引号**。 |
| `'unsafe-inline'` | **允许使用内联资源**。包括内联脚本 `javascript: URLs`、内联事件句柄、内联样式 `style`。**该取值必须有单引号**。 |
| `'unsafe-inline'` | 允许使用 `eval()` 或其他不安全的方法**根据字符串创建代码**。**该取值必须有单引号**。 |
|     `'none'`      | 空集，表示**没有任何源应该被匹配**。**该取值必须有单引号**。 |

#### 用例

|                             功能                             |                             代码                             |
| :----------------------------------------------------------: | :----------------------------------------------------------: |
|     所有内容均需来自**当前站点对应的源**，不涵盖其子域名     |        `Content-Security-Policy: default-src 'self'`         |
| 所有内容均需来自**受信任的域名及其子域名**，域名不必须与当前站点相同 | `Content-Security-Policy: default-src 'self' *.trusted.com`  |
| 所有内容均默认来自**当前站点对应的源**，除了 <br />① **图片可以从任意地方加载** <br />② **多媒体文件（音视频）仅允许从 `media1.com` 和 `media2.com` 加载**（不包括子域名）<br />③ **可执行脚本仅允许从 `userscripts.example.com` 加载**（不包括子域名） | `Content-Security-Policy: default-src 'self'; img-src *; media-src media1.com media2.com; script-src userscripts.example.com` |

#### 更多用法

CSP 可以通过 `Content-Security-Policy-Report-Only` HTTP 标头部署为**仅报告模式**，此时 CSP 的策略并**不是强制性的**，但是任何违规行为将会**报告**给一个指定的 URL 地址，该 URL 地址通过策略指令 `report-to` 指定。更多：[对策略进行测试](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/CSP#对策略进行测试)。

> 注意：截止 2024-09-26，MDN 关于 CSP 的解释中，中英文版本略有差异，请以英文版本为准。

### 3.3 服务端： Cookie 设置 HttpOnly 标志

> 适用于所有 XSS 攻击

由于 XSS 攻击多用于窃取用户的 cookie 数据，为了阻止恶意脚本 `document.cookie` 获取 cookie 值，服务端可以给其返回的 cookie 携带 `HttpOnly` 标志。浏览器会禁止页面的 JavaScript 访问带有 HttpOnly 标志的 cookie。

> 服务端通过 `Set-Cookie: <cookie-name>=<cookie-value>; HttpOnly` 响应一个携带 HttpOnly 标志的 cookie

<img src="https://cdn.jsdelivr.net/gh/Nasir1423/blog-img@main/image-20240926210026819.png" alt="image-20240926210026819" style="zoom:50%;" />

# 二、CSRF

## 1. 概述

CSRF（Cross Site Request Forgery）**跨站请求伪造**，指的是攻击者**冒充受信任的用户**，向被攻击网站的服务器发送**非预期请求**。CSRF 会导致用户的**登录态**被盗用，攻击者甚至会**冒充**用户操作或修改用户数据。

## 2. 分类

CSRF 攻击可分为三种：**Get 类型**、**Post 类型**、**链接类型**。

### 2.1 Get 类型

1. 概述：**Get 类型的 CSRF**，指的是：① 攻击者引诱用户进入**恶意网站**；② 恶意网站中自动向**用户已登录的网站服务器**发起 `Get` 请求，进行一些恶意操作。

   > Get 请求是**跨域**的，因此攻击者常通过 `<img>`、`<script>` 等标签绕过该限制

2. 示例

   ```html
   <!-- 当前页面是 attacker.com -->
   <!DOCTYPE html> 
   <html>
     <body>
       <h1>黑客的站点: CSRF攻击演示</h1>
   	<img src="https://example.com/sendcoin?user=hacker&number=100"> 
     </body>
   </html>
   ```

   假设用户已登录 `example.com`，攻击者引诱其打开 `attacker.com`。在该页面，攻击者将一个恶意链接（如转账请求接口）隐藏在 `<img>` 标签中，欺骗浏览器认为这是图片资源。当页面加载时，浏览器会自动发起一个 `GET` 请求。由于请求发送给 `example.com` 时携带了用户的登录态（如 Cookies），服务器会将其视为合法的转账请求，导致用户财产遭受损失。

### 2.2 Post 类型

1. 概述：**Post 类型的 CSRF**，指的是：① 攻击者引诱用户进入**恶意网站**；② 恶意网站中自动向**用户已登录的网站服务器**发起 `Post` 请求，进行一些恶意操作。

   > Post 请求是**跨域**的，因此攻击者常通过 `<form>` 等标签绕过该限制，其中 `<form>` 标签需要配合 JavaScript 自动提交

2. 示例

   ```html
   <!-- 当前页面是 attacker.com -->
   <!DOCTYPE html>
   <html>
     <body>
   	<h1>黑客的站点: CSRF攻击演示</h1>
   	<form id= 'hacker-form' action="https://example.com/sendcoin" method=POST>
   	  <input type="hidden" name="userll" value="hacker" />
   	  <input type="hidden" name="numberll" value="100" />
   	</form>
   	<script> document.getElementById ('hacker-form').submit(); </script> 
     </body>
   </html>
   ```

   假设用户已登录 `example.com`，攻击者引诱其打开 `attacker.com`。在该页面，攻击者将一个恶意链接（如转账请求接口）隐藏在 `<form>` 标签的 `action` 属性中。该表单是一个隐藏的表单，当页面加载时，表单自动提交，浏览器会自动发起一个 `Post` 请求。由于请求发送给 `example.com` 时携带了用户的登录态（如 Cookies），服务器会将其视为合法的转账请求，导致用户财产遭受损失。

### 2.3 链接类型

1. 概述：**链接类型的 CSRF**，指的是：① 用户点击攻击者提供的**恶意链接**；② 用户向**已登录的网站**发起了一个**意料之外**的 `Get` 请求，从而可能会涉及到一些恶意操作。

2. 示例：链接类型的 CSRF 常见于**邮件、图片、广告**等形式。

   ```html
   <div>
     <img width=150 src=http://images.xuejuzi.cn/1612/1-161230185104_1.jpg/> 
     <a href="https://time.geekbang.org/sendcoin?user=hacker&number=100" taget="_bla点击下载美女照片"/>
   </div>
   ```

## 3. 防御

因为 CSRF 是针对用户的请求伪造攻击，因此需要通过提高服务器的安全性来防护 CSRF 攻击。

### 3.1 服务端：Cookie 设置 SameSite 属性

我们知道，CSRF 攻击需要窃取用户的**登录状态**（通常为 cookie），然后冒充用户进行恶意操作。为了防止 cookie 在跨站请求中被发送，服务端可以为 cookie 配置 `SameSite` 属性，其取值及解释如下：

- **`Strict`**：浏览器仅在**同一站点**的请求中发送 cookie；如果请求来自不同的域名或协议，带有 `SameSite=Strict` 属性的 cookie 将不会被发送。

- **`Lax`**：cookie **不会在跨站请求中**发送，如加载图像或框架的请求；但当用户**从外部站点导航到源站**时（如点击链接），cookie 会被发送。这是未设置 `SameSite` 属性时的默认行为。

- **`None`**：浏览器在**跨站和同站请求中均会**发送 cookie。设置该属性时，必须同时设置 `Secure`，如 `SameSite=None; Secure`。

  > 有 `Secure` 标识的 cookie 仅在使用 HTTPS 协议发送加密请求时才会被发送到服务器，这也就意味着：非安全站点（`http:`）无法为 cookie 设置 `Secure` 指令，因此也无法使用 `SameSite=None`。

一般的，为了防范 CSRF 攻击，需要设置 cookie 的 `SameSite` 属性的值为 `Strict` 或 `Lax`。

> 服务端通过 `Set-Cookie: <cookie-name>=<cookie-value>; SameSite=Strict 或 Lax 或 None` 响应一个设置了 SameSite 属性的 cookie

### 3.2 服务端：验证 Referer 或 Origin 请求头

由于 CSRF 攻击多来自于**第三方站点**，从这个角度出发，可以在服务端进行**某些**操作**禁止来自第三方站点的请求**。一个可行的方式为，在服务端设置对请求报文中 `Referer` 或 `Origin` HTTP 的请求头的**检验**，从而判断请求是否合法。这里对这两个请求头进行介绍，

1. `Referer`：记录当前 HTTP 请求的来源地址（协议 + 主机 + 端口 + 路径）。

   ```bash
   Referer: https://developer.mozilla.org/zh-CN/docs/Web/JavaScript # 请求来源的协议 + 主机 + 端口号 + 路径
   ```

   > 注-1：由于 `Referer` 请求头记录的请求来源地址包括**请求路径**（path），因此可能会**泄露用户隐私**。
   >
   > 注-2：当 ① 请求来源地址采用的**协议**为本地的 `file` 或 `data` ② 当前请求的页面采用非安全协议，请求来源页面采用安全协议时，`Referer` 请求头不会被发送。

2. `Origin`：记录当前 HTTP 请求的来源地址（协议 + 主机[ + 端口] or null）。

   ```bash
   Origin: null # 表示请求来源是隐私敏感的
   Origin: https://developer.mozilla.org # 请求来源的协议 + 主机
   Origin: https://developer.mozilla.org:80 # 请求来源的协议 + 主机 + 端口号
   ```

   > 注-1：当请求是 ① **跨站请求** ② 除 `Get` 和 `Head` 以外的同源请求时，`Origin` 请求头会被发送。
   >
   > 注-2：相较于 `Referer` 请求头，由于不包含**请求路径**，`Origin` 请求头更加安全。

3. 服务端校验逻辑：1.st 优先基于 `Origin` 字段进行请求合法性校验；2nd. 如果没有 `Origin` 字段，则根据实际情况改为使用 `Referer` 字段进行请求合法性校验。

### 3.3 前端：CSRF Token 验证

CSRF Token 的生成与验证过程可以分为以下两个步骤：

**步骤 1**：浏览器向服务器请求一个页面，**服务器生成**一个 CSRF Token，并将其**嵌入**在返回的页面中。

```html
<!DOCTYPE html>
<html>
<body>
<form action="https://time.geekbang.org/sendcoin" method="POST">
    <input type="hidden" name="lcsrf-token" value="nc98P987bcpncYhoadjoiydc9ajDl">
    <input type="text" name="user">
    <input type="text" name="number">
    <input type="submit">
</form>
</body>
</html>
```

**步骤 2**：当浏览器需要向服务器发送其他请求时，必须携带页面中嵌入的 CSRF Token。服务器会验证该 CSRF Token 是否有效，从而决定是否响应该请求。

> 如果请求是从第三方网站发出的，则无法获取到 CSRF Token，因此即使发出了跨站请求，服务器也会因为 CSRF Token 不正确而拒绝该请求。

# 三、XSS Vs. CSRF

## 1. 攻击目标

1. XSS：攻击者注入**恶意脚本**到网页中 → **窃取用户信息**或**劫持用户会话**。
2. CSRF：攻击者引诱用户**在不知情的情况下向已认证的网站发送请求** → **利用用户的身份执行未授权操作**。

## 2. 攻击类型

1. XSS：**存储型**、**反射型**、**基于 DOM 型**
2. CSRF：**Get 类型**、**Post 类型**、**链接类型**

## 3. 防护措施

1. XSS：内容安全策略 CSP、输入输出过滤或转义、`HttpOnly` 的 Cookie
2. CSRF：`SameSite` 的 Cookie、`Referer` / `Origin` 验证、CSRF Token 验证

> **References**
>
> - [XSS 和 CSRF 攻击详解](https://juejin.cn/post/6945277278347591688)
> - [前端安全-XSS和CSRF](https://jacky-summer.github.io/2020/12/03/%E5%89%8D%E7%AB%AF%E5%AE%89%E5%85%A8-XSS%E5%92%8CCSRF/)
> - [内容安全策略（CSP） - HTTP | MDN](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/CSP)
> - [Set-Cookie - HTTP | MDN](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Headers/Set-Cookie#属性)
> - [Referer - HTTP | MDN](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Headers/Referer)
> - [Origin - HTTP | MDN](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Headers/Origin)

