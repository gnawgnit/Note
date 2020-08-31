# vim 插件管理

## 1.手动管理

将插件文件放到`~/.vim/bundle/`下，之后将在`.vimrc`中添加`runtimepath`。即

```vimrc
set runtimepath^=~/.vim/bundle/vim-markdown-quote-syntax-master
```

-----

## 2.插件管理(Vundle)

1. `git clone https://github.com/VundleVim/Vundle.vim`将Vundle.vim复制到`~/.vim/bundle/`目录下，之后将下面一段代码复制到`.vimrc`中。

   ```vim
   " 表明不与Vi兼容，因为如果与Vi兼容，很多强大的功能无法使用
   set nocompatible              " be iMproved, required
   filetype off                  " required
   
   " set the runtime path to include Vundle and initialize
   " running time path 的缩写，即我们到哪里去找插件
   set rtp+=~/.vim/bundle/Vundle.vim
   call vundle#begin()
   " alternatively, pass a path where Vundle should install plugins
   "call vundle#begin('~/some/path/here')
   
   " let Vundle manage Vundle, required
   Plugin 'VundleVim/Vundle.vim'
   
   " [Vim Markdown插件]
   " vim高亮显示Markdown语法
   Plugin 'morhetz/gruvbox'
   Plugin 'godlygeek/tabular'
   Plugin 'plasticboy/vim-markdown'
   
   " 不同形式的插件支持方式，各种形式的Plugin一定要在begin/end之间
   " The following are examples of different formats supported.
   " Keep Plugin commands between vundle#begin/end.
   
   " Github上的插件，直接写账户/项目名就可以
   " plugin on GitHub repo
   Plugin 'tpope/vim-fugitive'
   
   " vim-scriptes网站上插件
   " plugin from http://vim-scripts.org/vim/scripts.html
   Plugin 'L9'
   
   " 也是git仓库，但是不是Github上的插件，比如公司内的git仓库
   " Git plugin not hosted on GitHub
   Plugin 'git://git.wincent.com/command-t.git'
   
   ” 本地的插件形式
   " git repos on your local machine (i.e. when working on your own plugin)
   " Plugin 'file:///home/gmarik/path/to/plugin'
   
   " The sparkup vim script is in a subdirectory of this repo called vim.
   " Pass the path to set the runtimepath properly.
   Plugin 'rstacruz/sparkup', {'rtp': 'vim/'}
   
   " 同一个不同版本
   " Install L9 and avoid a Naming conflict if you've already installed a
   " different version somewhere else.
   " Plugin 'ascenator/L9', {'name': 'newL9'}
   
   " All of your Plugins must be added before the following line
   call vundle#end()            " required
   " 开启文件类型检测
   filetype plugin indent on    " required
   
   " To ignore plugin indent changes, instead use:
   "filetype plugin on
   "
   " Brief help
   " :PluginList       - lists configured plugins
   " :PluginInstall    - installs plugins; append `!` to update or just :PluginUpdate
   " :PluginSearch foo - searches for foo; append `!` to refresh local cache
   " :PluginClean      - confirms removal of unused plugins; append `!` to auto-approve removal
   "
   " see :h vundle for more details or wiki for FAQ
   " Put your non-Plugin stuff after this line
   ```

   

2. 打开vim，输入`:PluginInstall`安装插件或者在bash中输入`vim +PluginInstall +qall`。等待安装完成。

### Vundle使用

- Vundle help`h Vundle`

- 安装插件 `PluginInstall`
- 插件列表`PluginList`
- 插件查找`PluginSearch`
- 卸载插件`PluginClean`

**更多使用方法参考Vundle官方使用文档**