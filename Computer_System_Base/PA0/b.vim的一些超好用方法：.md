## Vim大法好：

#### 1.vim config：

- 到目前为止，接触Linux操作系统已经一年了，平时coding的时候也都是用vim，因此我愿称vim为最方便的编辑器(虽然学习成本有点高，自己目前也在不断学习中......)
- 接下来给出比较常用的vim编辑器配置：

```bash
if has("syntax")
	syntax on
endif
"首先把syntax打开，这是vim中的文本高亮。
setlocal noswapfile "取消文件的缓冲文件
set hidden "隐藏缓冲区
set number "在编辑器中显示行号
set cursorline "当前行高亮
set shiftwidth=4 "如果有自动缩进，则每次自动缩进四个空格
set softtabstop=4 "设置就好，不用知道什么意思
set tabstop=4 "设定一个tab建对应四个空格
set hlsearch "检索高亮
set magic "设置开启魔术，不知道干啥的

"下面这些键位设置是在coding的时候更加人性化，因为一开始用windows的编辑器比较多，有括号等补全功能，所以在vim中同样设置括号补全等功能
inoremap " ""<Esc>i 
inoremap [ []<Esc>i
inoremap ' ''<Esc>i
inoremap ( ()<Esc>i
inoremap > ><Esc>i
inoremap { {<CR>}<Esc>O
```

#### 2.vim常用命令：

- 将光标移动文本开头：
  - 在普通模式下：``gg``
- 将光标移动文本结尾：
  - 在普通模式下：``G``
- 将光标移动至当前行首：
  - 在普通模式下：``0``
- 将光标移动至当前行尾：
  - 在普通模式下：``$``
- 定位到某一行：
  - 在普通模式下：``行号+gg``
- 删除某一行：
  - 在普通模式下：``dd``
- 复制某一行：
  - 在普通模式下：``yy``
- 将删除或复制的内容粘贴在光标的下一行：
  - 在普通模式下：``p``
- 撤销上一步的动作：
  - 在普通模式下：``u``

#### 3.vim的惊人用法：

- 同时以编辑模式打开多个文件(该操作非常适合处理工程文件)：
  - ``vim -p file_1 file_2``；其中-p表示以编辑模式打开。
  - ``vim -p *``；其中*指代当前目录下的所有文件。
  - 在使用这个功能时，我们通常配合``touch``命令，使用``touch``来创建空文件，然后使用vim打开进行编辑：
    - ``touch file_1.c file_2.c``；创建两个空文件。
    - ``vim -p file_1.c file_2.c``；使用vim同时对这两个文件进行编辑。

