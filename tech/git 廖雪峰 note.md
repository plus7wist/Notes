## git 诞生

传说在 Linus 创造 linux 的时候，由于这是个完全开源的系统，参与其开发的不仅有 Linus 等名人，也有许多默默无闻的志愿者。这些热心人把代码文件通过 diff 的方式发给 Linus，然后 Linus 本人通过手工的方式把代码合并起来。

为什么 Linus 使用这种原始的方式而不是使用 CVS、SVN 这些版本管理软件呢？因为这些**集中式**的版本控制软件不但速度慢，而且必须连接互联网。另外一些商用的版本管理软件，虽然比上述两者好用，但是违背了 Linus 的开源精神。

不过，到了 2002 年，Linux 系统已经发展了十年了，代码库之大让Linus很难继续通过手工方式管理了，社区的弟兄们也对这种方式表达了强烈不满，于是Linus选择了一个商业的版本控制系统 BitKeeper，BitKeeper 的东家 BitMover 公司出于人道主义精神，授权 Linux 社区免费使用这个版本控制系统。

安定团结的大好局面在2005年就被打破了，原因是 Linux 社区牛人聚集，不免沾染了一些梁山好汉的江湖习气。开发Samba的Andrew试图 破解BitKeeper的协议（这么干的其实也不只他一个），被BitMover公司发现了（监控工作做得不错！），于是BitMover公司怒了，要收回Linux社区的免费使⽤用权。

Linus 向 BitMover 公司道了个歉，保证以后严格管教弟兄们，嗯，这是不可能的。实际情况是这样的：

Linus 花了两周时间**自己**用C写了一个分布式版本控制系统，这就是Git！一个月之内，Linux 系统的源码已经由Git管理了！牛是怎么定义的呢？大家可以体会一下。

Git 迅速成为最流行的分布式版本控制系统，尤其是 2008 年，GitHub 网站上线了，它为开源项目免费提供 Git 存储，无数开源项目开始迁移至GitHub，包括 jQuery，PHP，Ruby 等等。

历史就是这么偶然，如果不是当年 BitMover 公司威胁 Linux 社区，可能现在我们就没有免费而超级好用的Git了。

## 安装 git

### Linux

```
> git
The program 'git' is currently not installed. You can install it
by typing:
> sudo apt-get install git
```

如果你碰巧用Debian或Ubuntu Linux，通过一条“ sudo apt-get install git ”就可以直接完
成Git的安装，非常简单。

老一点的Debian或Ubuntu Linux，要把命令改为“sudo apt-get install git-core”，因为以前有个软件也叫GIT（GNU Interactive Tools），结果Git就只能叫git-core了。由于Git名气实在太大，后来就把GNU Interactive Tools改成gnuit，git-core正式改为git。

如果是其他Linux版本，可以直接通过源码安装。先从Git官网下载源码，然后解压，依次输入：./config，make，sudo make install这几个命令安装就好了。

### MAC OS X

推荐安装 XCode，其中集成了 git，但是没安装，在插件里找一下就可以了。

XCode/Preferences/Downloads/Command Line Tools(大概 100+MB)，安装即可。

### Windows

http://msysgit.github.io/ 下载 msysgit，安装。Git/Git bash，弹出命令窗口说明安装成功。

在 git 命令窗口里面设置：

```
> git config --global user.name "$user-name"
> git config --global user.email "$user-email"
```

$user-name，$user-email 对应你的用户名和电邮。

--golbal 表示默认对你电脑上的所有仓库使用这个配置。不过不用担心，这只是一个默认值而不是一个固定值，你可以轻易的对不同的仓库使用不同的配置。

## 创建版本库

版本库是一个目录，git 可以管理里面的所有文件。文件的修改删除等等 Git 都可以跟踪、还原。

```
> mkdir $git-dir
> cd $git-dir
> git init
Initialized empty Git repository in /Users/michael/learngit/.git/
```

上述使用一个新建的目录创建了版本库。$git-dir 是版本库的名字——当然也是一个文件夹的名字。你可以使用 learngit、bloggit 等等你愿意的名字。

**注意** 文件应该注意编码，如果没有历史遗留问题，请使用 utf-8。


### 添加版本

在 $git-dir 里面建立一个文件 $file-01，比如叫做 README.md 的文本文件（这个名字的文件大多是用来解释这个目录里的内容的）。

```
> git add $file-01
> git commit -m "$msg-file-01"
  [master (root-commit) cb926e7] wrote a readme file
  1 file changed, 2 insertions(+)
  create mode 100644 $file-01
```

`git add` 把文件送到暂存区，`git commit` 把暂存区的文件提交给版本库。

add-commit 把文件提交给 git 管理，一次 commit 算作是一个版本，-m 参数后面的字符串 $msg-flie-01 用于描述这个版本。

**注意**，如果你使用 windows 编辑程序，应该注意到文本格式的换行在 windows 下是 CRLF，但是其他系统下都是 LF。add 的时候会报告：

```
warning: LF will be replaced by CRLF in $file-x.
The file will have its original line endings in your working directory.
```

具体你想要换行符使用什么格式，使用如下三条命令中的一条。

```
> git config --global core.autocrlf true  # 签出代码时，LF会被转换成CRLF
> git config --global core.autocrlf input # 签出时不转换
> git config --global core.autocrlf false # 把 CRLF 记录在库中
```

## 版本时间线

修改 $file-01 的内容，保存，之后使用 `git status` 查看结果。git 会告诉你 $file-01 修改过，但是没有提交。

使用 `git diff $file-01` 可以查看具体修改了什么（跟上次的区别）。红色行用 - 开头，表示你删除的内容；绿色行用 + 打头，表示你添加的内容。

### 版本记录

使用 `git log` 查看仓库的提交记录，提交记录是按照最新版本优先排序的列表，每一项有如下内容：

```
commit $commit-id
Author: $user-name <$user-email>
Date: $commit-time
  $commit-msg
```

$commit-msg 值取自：`git commit -m $commit-msg`

### 版本回退

HEAD 表示当前版本，前一个版本是 HEAD^，HEAD^^ 指的是上上个版本，HEAD~10 表示是上行 10 个版本。

命令：`git reset --hard $version` 使得当前仓库退回到从前的版本。$version 可以是 HEAD^ 等标识，也可以是 `git log` 里出现的 $commit-id，对于后一种情况，你可以只使用前面几位 id（这个 id 很长），git 会自动查找匹配的版本，有冲突会提示你。

回退之后使用 `git log` 会发现新的版本记录已经没了。如果你想撤销回退，可以先使用 `git reflog` 命令。这个命令查看的是你的操作记录（是以版本为单位的，add 之类命令不会记录），由此可以找到新版本的 $commit-id 于是可以撤销回退。

## 检出文件

`git reset` 作用于版本库文本变化。你可以使用 `git checkout -- $file-x` 来使得 $file-x 回退到暂存区或者版本库中的最近版本。

如果你要这个文件回退到以前某个版本的内容，应该先 reset 回退版本库，再 checkout。
