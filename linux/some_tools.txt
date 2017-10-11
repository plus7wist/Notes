# 那些工具

## Atom

官网上有 deb；ppa 也是可以的。

```sh
sudo add-apt-repository ppa:webupd8team/atom  
sudo apt-get update   
sudo apt-get install atom
```

atom 出身 github，但是我用的还不多。atom 常常与 sublime text 比较。atom 的中文支持比 sublime 好（特别是 linux 下）；atom 背后是整个 github，插件肯定有很多选择；sublime text 原生有对 vim 的支持，但是 atom 好像没有。

我前几日试用了 atom，主要用来写笔记（markdown）。atom 原生有插件 markdown-preview，但是不怎么好用。

推荐 markdown-preview-enhanced，使用 atom 的插件管理就可以方便的安装。如果你想下载安装的话就这样做：

```sh
cd ~/.atom/packages
git clone git@github.com:shd101wyy/markdown-preview-enhanced.git
cd markdown-preview-enhanced
apm install # 耐心等待……
```

耐心等待的意思是这个插件有点大（32M 左右……），当然使用体验是很好的。自定义方面，可以在 less 里面修改，我主要改动一下字体。

另外大可把原来的 markdown-preview 禁用，此外还有 spell-check 插件，多数时候也是用不着的。

## uget+aria2

linux.cn 的[这篇文章](https://linux.cn/article-7369-1.html)介绍了 linux 下十大下载工具，有空我再看看……

我还是选择了标题上的这两个。

```sh
sudo add-apt-repository ppa:plushuang-tw/uget-stable
sudo apt-get update
sudo apt-get install uget
sudo add-apt-repository ppa:t-tujikawa/ppa
sudo apt-get update
sudo apt-get install aria2
```

uget 的设置/插件中选择使用 aria2。

## zsh

一个不是很常用的 shell，但是由于 oh-my-zsh 而变得流行了……

```sh
sudo apt install zsh
```

## oh-my-zsh

```sh
git clone git://github.com/robbyrussell/oh-my-zsh.git ~/.oh-my-zsh
cp ~/.oh-my-zsh/templates/zshrc.zsh-template ~/.zshrc
chsh -s /bin/zsh # 设 zsh 为默认 shell
```

.zshrc 文件里的 `ZSH_THEME` 改成喜欢的样式名字，我最近喜欢 ys 这个样式，理由有两个：显示了时间，感觉很实用；输入位置在第二行，路径长了不用输入一点命令就换行。

## tree

终端工具，画出目录的结构，就像这样。

```sh
$ tree .recommenders
.recommenders
├── caches
│   ├── identified-project-coordinates.json
│   └── manual-mappings.json
└── index
    └── http___download_eclipse_org_recommenders_models_neon_
        ├── _3.fdt
        ├── _3.fdx
        ├── _3.fnm
        ├── _3.frq
        ├── _3.nrm
        ├── _3.prx
        ├── _3.tii
        ├── _3.tis
        ├── segments_4
        └── segments.gen

3 directories, 12 files
```
