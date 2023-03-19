# 一网盟 Hugo 仓库使用说明
本仓库为hexo网站源码，其中可能包含私密信息，请务必设置仓库可见性为 `Private` 。
## 功能简介
1. 本仓库有提交变更则自动触发渲染 HTML
2. 本地端不需要渲染和发布工序，只需要维护 MarkDown 源文档，提交同步到 GitHub 云端仓库即可
3. HTML 静态页自动发布到：`owner.github.io` 「需自行建立 pages 仓库和配置授权」，分支：`pages-hugo`
4. 如果网址非 `github.io`，则自动生成 `CNAME` 「需自行在DNS托管商处做好cname解析」
   
![本仓库方案](https://cdn.jsdelivr.net/gh/828767/static/images/github_page_free.png)

## 本地预览环境
为更好地预览即将发布的内容，建议将本仓库克隆到本地电脑维护 MarkDown 源码，那么本地就需要安装一个预览环境。

> 到以下涉及软件官网下载如果速度慢，可以从 [墙内淘宝源下载](https://registry.npmmirror.com/binary.html)。

### **git**
大名鼎鼎的代码项目管理工具，到 [Git-SCM官网](https://git-scm.com/downloads) 或 [墙内淘宝源](https://registry.npmmirror.com/binary.html?path=git-for-windows/ "Windows版，其他系统自带或直接命令安装") 下载安装包或者软件源默认安装完成即可。

仓库同步就需要通过 `git` 客户端，Windows 系统安装完成后，会在右键菜单添加 `Git Bash Here` 入口，方便后续使用。

![Git Bash Here](https://cdn.jsdelivr.net/gh/828767/static/images/git_menu_gitbashhere.png)

如果以前未使用过 Git，一般都需要设置用户名和邮箱，随便一个目录空白地方 点右键「Windows系统，其他系统打开系统终端输命令」》 `Git Bash Here` ，运行以下命令设置：
```bash
git config --global user.name name #设置Git用户名
git config --global user.email "email" #设置Git邮箱
```
> 这里只是最基本的Git信息设置，后续提交同步 GitHub 等需要额外授权另外教程再说，或者自行求助战略合作伙伴 Google 或百度。


### **nodejs**
`hugo` 虽然对环境没有依赖，但很多主题依旧引入 `npm` 套娃，所以根据主题文档要求来，或者无脑直接装个 `nodejs` 也不是不可以。

`nodejs` 是跨平台的 JavaScript 运行环境和包管理工具。同样的，到 [Nodejs官网](https://nodejs.org/zh-cn/)  或 [墙内淘宝源](https://registry.npmmirror.com/binary.html?path=node/) 下载安装包，建议选择长期维护版，默认安装完成即可。

安装完成后，在前文安装完成的 `Git Bash` 或者系统终端中输入命令 `npm version` 验证安装结果：
```bash
$ npm version
{
  npm: '8.5.5',
  node: '16.15.0',
  ……
}
```

为了后面安装依赖包顺利完成，运行以下命令设置 npm 淘宝源：
```bash
# 墙内设置 npm 淘宝源，加快网络下载速度，墙外就不要做了
npm config set registry https://registry.npm.taobao.org
```

### **hugo**

Hugo 执行程序就是一个单文件，可以不依赖外部环境独立运行。到 [官方版本库](https://github.com/gohugoio/hugo/releases/latest) 下载对应操作系统的可执行程序，解压放到系统目录或者解压到某个目录后添加系统变量路径即可。

以 Windows 系统为例，下载 `hugo_extended_0.108.0_windows-amd64.zip` ，将压缩包内 `hugo.exe` 解压出来，然后移到系统目录如 `c:\windows` ，一步就完成了，也不用麻烦添加系统变量。

> Hugo is available in two editions: standard and extended. With the extended edition you can:
>
> - Encode WebP images (you can decode WebP images with both editions)
> - Transpile Sass to CSS using the embedded LibSass transpiler
>
> We recommend that you install the extended edition.
>
> 官方建议下载 `_extended` 版本

放置完程序可以打开 `Git Bash` 或者随便开个终端，运行 `hugo` 命令验证：
```bash
$ hugo version
hugo v0.108.0-a...d+extended windows/amd64 BuildDate=202...Info=gohugoio
```

### **项目源码仓库**
前面的准备工作已完成，剩下就是将项目源码仓库文件克隆同步到本地电脑，还是在 `Git Bash` 中，输入这样的命令：
```bash
cd d:\Git   #先切换到要存放Git文件的目录路径，vscode终端会自动切换到启动时所在目录
git clone --recurse-submodules 自己的仓库地址 #带子模块一起克隆
```

待仓库克隆完成，整个本地预览环境就全部安装完成了，在仓库根目录路径下运行 `hugo server` 即可启动预览服务：
```bash
xyz@IAY MINGW64 /d/Git/action-hugo (main)
$ hugo server
Start building sites … 
hugo v0.108.0-a0d64a46e36dd2f503bfd5ba1a5807b900df231d+extended windows/amd64 BuildDate=2022-12-06T13:37:56Z VendorInfo=gohugoio

                   | EN | FR  
-------------------+----+-----
  Pages            | 22 | 22
  Paginator pages  |  1 |  1
  Non-page files   |  0 |  0
  Static files     | 71 | 71
  Processed images |  0 |  0
  Aliases          |  5 |  4
  Sitemaps         |  2 |  1
  Cleaned          |  0 |  0

Built in 372 ms
Watching for changes in D:\Git\action-hugo\{archetypes,content,data,i18n,layouts,static,themes}
Watching for config changes in D:\Git\action-hugo\config.toml
Environment: "development"
Serving pages from memory
Running in Fast Render Mode. For full rebuilds on change: hugo server --disableFastRender
Web Server is available at http://localhost:1313/ (bind address 127.0.0.1)
Press Ctrl+C to stop
```

以上输出信息中，`/d/Git/action-hugo (main)` 就是所谓运行路径，Windows系统表示 `d:\Git\action-hugo` 目录，当前在 `main` 分支。

`EN | FR` 表示有双语内容，浏览器中打开 `http://localhost:1313/` 就可以预览，按 `Ctrl+C` 组合键停止，一些主题或者网站设置变更需要重启该预览服务才能看到效果。

为了更好地理解 `hugo` 网站，建议了解下 `hugo` 站点目录结构：
```toml
example.com/
├── archetypes/ # 模板文件夹
│   └── default.md # 默认模板
├── assets/ # 默认不会创建，Stores all the files which need be processed by Hugo Pipes. Only the files whose .Permalink or .RelPermalink are used will be published to the public directory.
├── content/ # 内容目录，相当于网站根目录，网络路径：/
├── data/ # 存放数据配置文件
├── layouts/ # HTML模板
├── public/ # 发布目录，渲染后的HTML文件存放与此，仓库版本地不需要渲染发布动作
├── static/ # 静态资源文件夹
│   └── images # 自建存图片目录
│       └── hugo.jpg # 网络路径：/images/hugo.jpg
├── themes/ # 主题目录
└── config.toml # 最重要的网站配置
```

## 编辑器推荐
工欲善其事必先利其器，一个编辑器可以事半功倍，VSCODE 就是个不错的选择，自行到 [微软官方网站](https://code.visualstudio.com/download) 去下载安装，优点：
1. 全目录管理，一个界面可以管理整个目录下的文件
2. 语法格式显示，也能实时预览
3. 与Git集成，可以界面化操作Git提交同步，比较等
4. 集成命令终端，预览调试方便
 
![VSCODE](https://cdn.jsdelivr.net/gh/828767/static/images/vscode-hexo.png)

其他如 Atom、Sublime Text、Typroa 之类的编辑器，甚至是专业的代码编辑器请自行研究。

作为MarkDown编辑器，建议安装以下插件：
1. Git History
2. GitLens supercharges
3. Markdown All in One
4. Markdown Preview Mermaid Support
5. Markdown Table
6. Markdown Shortcuts

其他有用的插件请自行探索。

## 其他事项
1. 任何增删改都需要提交同步到本仓库，同步后上端会自动处理，等几分钟刷新缓存就能看到效果了
2. 提交前可以先本地预览，效果满意了再提交同步到上端仓库
3. 根目录下的 `config.toml` 为网址基础配置，主题内容相关的配置请根据主题要求填充配置
4. Git基础用法和MarkDown语法等很多基础知识都可以自行求助战略合作伙伴 Google 或百度，遇问题解决问题
5. 关于怎么用入门教程汇总可以参考：[从零开始建个Hexo小站](https://yiwangmeng.cn/action-hexo/guide-how-to-build-site-0.html)「就不单独写hugo教程了，除了命令不一样其他大同小异」


## Stargazers over time

![Stargazers over time](https://starchart.cc/828767/action-hugo.svg)
