

参考地址：
- [Learn Vim](https://github.com/wsdjeg/Learn-Vim_zh_cn/blob/master/README.md)
- [github](https://github.com/wsdjeg/Learn-Vim_zh_cn)
- [自学指南](https://csdiy.wiki/%E5%BF%85%E5%AD%A6%E5%B7%A5%E5%85%B7/Vim/)
- [Vim 从入门到精通](https://gitlab.com/wsdjeg/vim-galore-zh_cn)
- [精通 VIM 此文就够了](https://zhuanlan.zhihu.com/p/68111471)

### 认识 Vim

vim 常用的四个模式：
- 正常模式 (Normal-mode) - 敲击键盘执行 `vim` 命令，可以执行复制、粘贴、删除等操作。
- 插入模式 (Insert-mode) - 按 `i` 进入该模式，敲击键盘可以编辑修改文件内容。
- 命令模式 (Command-mode) - 按 `:` 或者 `/` ,可以执行一些命令
- 可视模式 (Visual-mode) - 按 `v`,`V`,`<Ctrl>+v` ，很像鼠标右键选择的感觉。

> 通过 `<ESC>` 可以退出模式，回到正常模式。

#### 帮助文档

```bash
:help
:h CTRL-P # 普通模式下，关于 Ctrl-P 的介绍
:h i_CTRL-P # i_ 表示插入模式；插入模式下，关于 Ctrl-P 的介绍
```

#### Vimrc 

它是 Vim 的配置文件，

### Vim 显示区域

- Buffers
- Windows
- Tabs

### 基础 01

```bash
vim # 打开vim
:quit # 退出
:write # 保存修改
# 命令简写
:wq # 保存并退出
:q! # 强制退出

```



### 搜索文件


### 打开文件

- `vim fileName`
- `:edit fileName`
- `:find path`

配置 `path`

```bash
:set path+=app/controllers/**
```

将整个项目文件夹添加到`path`中，当您按`<Tab>`，Vim 将在所有文件夹内搜索文件。

```bash
:set path+=$PWD/**
```
`$PWD` 表示当前工作目录，表示将整个项目路径加到`path`中，并让所有文件名可以用`<Tab>`补全。

解决 windows 系统设置不生效的问题

```bash
let $PWD=getcwd() # 解决 windows 不生效的问题
```

### 搜索文件

- 内置grep `:vim`，它是`:vimgrep`的简写
- 外部grep `:grep`

```bash
:vim /pattern/ file # pattern:正则表达式；file：文件参数。

# 示例: 查找 app/controllers 目录中，文件名包含字符串 breakfast 的文件
:vim /breakfast/ app/controllers/**/*.rb
```

搜索完会打开第一个结果，运行`:copen` 浏览所有文件
```bash
:copen        打开quickfix窗口
:cclose       关闭quickfix窗口
:cnext        跳到下一个错误
:cprevious    跳到前一个错误
:colder       跳到旧的错误列表
:cnewer       跳到新的错误列表
```

如果找到大量文件，内置grep会很慢，使用外部grep
```bash
# 查找 app/controllers 目录中，文件名包含字符串 lunch 的文件
:grep -R "lunch" app/controllers/ 
```

设置 Netrw 浏览文件

```bash
set nocp
filetype plugin on
```

`netrw` 命令修改文件夹

```
%    创建新文件
d    创建新目录
R    重命名文件/目录
D    删除文件/目录
```

Fzf 搜索插件

依赖：[fzf](https://github.com/junegunn/fzf)和[ripgrep](https://github.com/BurntSushi/ripgrep)
- `fzf`: 多用途的命令行模糊搜索工具
- `ripgrep`: 类似`grep`的搜索工具

```bash
brew install fzf ripgrep
```

设置 `fzf` 使用 `ripgrep`

```bash
# .zshrc 文件
if type rg &> /dev/null; then
  export FZF_DEFAULT_COMMAND='rg --files'
  export FZF_DEFAULT_OPTS='-m'
fi
```

`fzf`语法：
- `^` 表示前缀精确匹配。要搜索一个以"welcome"开头的短语：`^welcom`。
- `$` 表示后缀精确匹配。要搜索一个以"my friends"结尾的短语：`friends$`。
- `'` 表示精确匹配。要搜索短语"welcom my friends"：`'welcom my friends`。
- `|` 表示"或者"匹配。要搜索"friends"或"foes"：`friends | foes`。
- `!` 表示反向匹配。要搜索一个包含"welcome"但不包含"friends"的短语：`welcome !friends`。

您可以混合起来使用。比如，`^hello | ^welcome friends$`将搜索以"welcome"或"hello"开头，并且以"friends"结束的短语。

**vim中使用:** 
- 查找文件`:Files`，您将看到fzf搜索提示符
- 映射到`Ctrl + F` 
```bash
# .vimrc 文件
nnoremap <silent> <C-f> :Files<CR>
```
- 在文件中查找`:Rg`
- 映射到`<Leader>f`
```bash
# .vimrc 文件
nnoremap <silent> <Leader>f :Rg<CR>
```
- [其他映射建议](https://github.com/wsdjeg/Learn-Vim_zh_cn/blob/master/ch03_searching_files.md#%E5%85%B6%E4%BB%96%E6%90%9C%E7%B4%A2)

### [在多文件中搜索和替换](https://github.com/wsdjeg/Learn-Vim_zh_cn/blob/master/ch03_searching_files.md#%E5%9C%A8%E5%A4%9A%E6%96%87%E4%BB%B6%E4%B8%AD%E6%90%9C%E7%B4%A2%E5%92%8C%E6%9B%BF%E6%8D%A2)


### Vim 插件管理器
- [vim-plug](https://github.com/junegunn/vim-plug)
- Q: `filetype plugin indent on` and `syntax enable`. 和 `vim-plug`有什么关系？

### Vim 语法

Motion

```
h	左
j	下
k	上
l	右
w	向前移动到下一个单词的开头
}	跳转到下一个段落
$	跳转到当前行的末尾
```

Operator（操作符）

根据`:h operator`，Vim共有16个**操作符**，然而根据我的经验，学习这3个**操作符**在80%的情况下就已经够用了

```
y	yank(复制)
d	delete(删除)
c	change 删除文本，将删除的文本存到寄存器中，进入插入模式
```

Operator + motions

- 复制当前位置到行尾的所有内容：`y$`
- 删除当前位置到下一个单词的开头：`dw`
- 修改当前位置到这个段落的结尾：`c}`

motions + 数字
- 向左拷贝2个字符：`y2h`
- 删除后两个单词：`d2w`
- 修改后面两行：`c2j`

### Text Objects (文本对象)

- 删除括号内部的内容但保留括号：`di(`
- 删除括号以及内部的内容：`da(`

下面列举的一些通常见到的文本对象：

```
w     一个单词
p     一个段落
s     一个句子
(或)  一对()
{或}  一对{}
[或]  一对[]
<或>  一对<>
t     XML标签
"     一对""
'     一对''
`     一对``
```

通过`:h text-objects`了解更多

### [结合性和语法](https://github.com/wsdjeg/Learn-Vim_zh_cn/blob/master/ch04_vim_grammar.md#%E7%BB%93%E5%90%88%E6%80%A7%E5%92%8C%E8%AF%AD%E6%B3%95)

### 文件移动

从`h,j,k,l,w,b,G,/,?,n`开始，不断地重复这10个移动知道形成肌肉记忆。
