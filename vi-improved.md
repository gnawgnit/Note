# vi-improved (vim)学习

[TOC]

## 1.单词

- abort: 使流产，使夭折，使中止；
- append 附加，添上；
- familiar 熟悉的，通晓的；冒昧的，随便的；
- configurable 可配置的；
- indicate 表明，指示，暗示；
- modified 改良的，改进的，修改的；
- scrolling 上下滚动；
- syntax 语法规则，句法，句构；
- shortcut 捷径，被截短的东西；
- picky 吹毛求疵，好挑剔的，过分讲究的；
- distinction 区别，特质，卓越；
- specifically 明确地，特有地；
- illustrate 说明，表明；
- entire 整个的，全部的，整行的；
- instance 实例，例子；
- execute 执行，履行；
- versa 反的；
- vice 不道德的行为，缺点；
- macros 宏命令；
- digraph 连字；

## 2.命令

`fx`to search a character x

ps:光标停在该字符上

F与其查找方向相反

`tx`命令和其类似，但光标停在该字符的前面

T方向与其相反，且光标停在该字符的后面

`d$`与`D`一样

`c$`和`C`一样

**The . command is one of the most simple yet powerful commands in Vim. It repeats
the last *delete or change* command.**

i -> insert	a->append	J->joining line R->replace	d->delete	c->change	p->paste	y->yank	e->end_of_word

w->world	t->till	f->find	 



`~`命令进行字母大小写反转，如果遇到数字或其它符号就跳过，即光标跳到下一字符。

`@character` 宏命令：普通模式下按q+字符（a-z）该字符使宏的寄存器名称，接着输入命令，按q停止。之后按@+寄存器名称调用。