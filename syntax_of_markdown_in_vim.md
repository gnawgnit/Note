# vim中markdown语法高亮的设置

随着vim版本发布的配置文件中，有很多vim脚本用于各种语言的高亮设置，其中就有markdown.vim（VIMRUNTIME/ftplugin/markdown.vim，VIMRUNTIME一般不设置为系统环境变量，但是可以在vim中使用`:echo $VIMRUNTIME`来查看具体路径，这个变量是默认随版本发布时就设置好的。另外，runtimepath(rtp)是用户自定义的，可以用`set rtp`查看具体设置，一般包括VIMRUNTIME）。可以借用VIMRUNTIME中的目录结构，用在\~/.vim中，形成自定义的配置vim的目录，之后设置runtimepath包含该目录。将VIMRUNTIME/ftplugin/markdown.vim复制到\~/.vim/ftplugin/中，在\~/.vimrc（自定义的vim运行时文件）中添加相关配置语句：

```bash
augroup vimrcEx
	autocmd!
	
	"特定文件的语法高亮
	autocmd BufRead,BufNewFile *.md set filetype=makedown
	"启用Markdown拼写检查
	autocmd FileType markdown setlocal spell
	"一行只显示80个字符
	autocmd BufRead,BufNewFile *.md setlocal textwidth=80
augroup END
```

之后就可以有markdown的语法高亮，拼写检查功能了。

本来只要打开syntax开关就可以了，但是因为markdown.vim这个文件要求后缀名为.markdown。但是现在一般使用后缀名.md。所以打开后没有语法高亮。上面的文件可识别.md后缀。

**使用Vundle安装markdown代码块内的语法高亮**

插件：[https:github.com/joker1007/vim-markdown-quote-syntax.git](https://github/joker1007/vim-markdown-quote-syntax.git)

将以上url放到\~/.vimrc中Vundle相关配置下：`Plugin 'https://github.com/joker1007/vim-markdown-quote-syntax.git'`。之后PluginInstall就行了。