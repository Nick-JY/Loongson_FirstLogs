## tmux —— 专注于分屏的神器：

### 1.tmux简介：

- ``tmux``这一款工具可以处理分屏操作，这里就会有人说，直接在Linux中多开几个Terminal不就可以了吗，回答的显然太早了些，如果有些程序需要后台挂起，那么使用tmux是最佳的选择(可以关闭Terminal，但后台进程不会挂断)
- 把Clash运行在了tmux的session上......，相当舒适......

#### 2.tmux的使用：

- 我们要分清，在tmux中可以有session和window之分，一个session可以创建多个window，通常我们把一个后台程序运行在一个session上。
- 创建session：
  - ``tmux new -s name``其中，name是session的名称，用户自定义。
- 在session中创建一个window：
  - 快捷建：``先按ctrl + b ，然后按c``
- 切换window：
  - 快捷键：``先按ctrl + b ，然后按w``，之后便能显式的切换所有session中的window。
- 将某一个session挂起(挂起之后该session会在后台运行)：
  - 快捷键：``先按ctrl + b ，然后按d``，之后便将该session挂起。
  - 在tmux引出的Terminal中输入command：``tmux detach``，完成该session的挂起操作。

- 查看所有的session信息:
  - 无论是在Terminal还是在某个session中：``tmux ls``
- 杀死某个session中的window：
  - 在该session中：``tmux kill-window -t 编号``编号是当前window的编号。
- 杀死某个session：
  - 1.快捷键：如果在该session中：``ctrl + d``
  - 2.无论是在Terminal还是在该session中：``tmux kill-session -t 名称``名称是session的名称。
  - 3.在该session中，显式的输入：``exit``