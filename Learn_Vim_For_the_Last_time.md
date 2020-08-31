# Learn Vim For the Last time

**You must believe that vim is a language, so you just learn a language.**

## Basic 

## A few changes of Configure:

### Exit Insert

Vim is about efficiency, and it's hardly efficient to leave the home keys if you don't have to. So don't.

`inoremap jk <ESC>`



### Changing the leader key.

The leader is an activation key for shortcut, and it's quite powerful.

The default leader () key seems rather out of the way as well, so I like to remap the leader key to `Space`.

`let mapleader = " "`

Now when you executing your nifty(精巧的) shortcuts that you are about learn, you can do so with either thumb(大拇指)，since your thumb are always on the `Space` bar.



### Remapping Capslock(大小写转换)

Generally, the `Capslock` key on a keyboard is worthless to me, so I remap it to `Ctrl`.So my left pinky can simply slide to the left by on key to executing `Ctrl-whatever`.



Then there are just a few basics that are recommended by most and make things much easier overall.

`filetype plugin indent on`
`syntax on`
`set encoding=utf-8`
`set clipboard=unnamedplus`

(The "unnamedplus" option maps your system keyboard to Vim's paste buffer)

Remember, you can spend a lifetime to optimizing(优化) your `~/.vimrc` file.



### Plugin Management

**Native management**

The Vim 8.x supports native plugin management, you simply drop your plugins under:

`~/.vim/pack/pluginfoldername/ start/pluginname`, Done and done. Now you can play with any plugins you want using the method above and they will be loaded automatically when Vim starts. 



### Use git management/stored the ~/.vim directory

Then you can git clone the entire directory to your new box, of course, need Network.



## Vim as language

Arguably the most brilliant thing about vim is that you use it you begin to think in it. Vim is set up to function like a language, complete with nouns, verbs, and adverbs. 



### verbs

Verbs are the actions we take, and they can be performed nouns.Example:

`d: delete`

`c:change`

`y:yank`

`v:visually select`



### modifiers(修饰词)

Modifiers are used before nouns to describe the way in which you are going to do something. Example:

`i:inside`

`a:around`

`NUM:number`

`t:search for something and stop before it`

`f:search for that thing and lands on it`

`/:find a string(literal or regex)` 



### nouns

In English, nouns are objects you do something to. They are objects in Vim too. Example:

`w:word`

`s:sentence`

`):sentence(anther way of doing it)`

`p:paragraph`

`}:paragraph(another of doing it)`

`t:tag(think HTML/XML)`

`b:block`



### nouns as motion

You can also use nouns as motions, meaning you can move around your content using them as the size of your jump.



### using this language

#delete two words

`d2w`

#change inside sentence(delete the current one and enter insert mode)

`cis`

#yank inside paragraph(copy the paragraph you are in)

`yip`

#change to open bracket(change the text from where you are to the next open bracket`<`)

`ct<`

So it's intuitive and elegant(直观和优雅的)and like any other language the more you use it the more naturally it will come to you.



## Getting things done

### working with your file

Some quick basic on working with your file.

`vim file` open your file in vim

`:w` write your changes to the file

`:q!` get out of vim(quit), but without saving your changes(!)

`:saveas ~/some/path/` save your file to that location vim

`ZZ` a fast way to do `:wq`



### search your text

**searching by string**

One of most basic and powerful ways to search in `vim` is to enter the "/" command, which takes you to the bottom of your window, and then type what you're looking for and press `ENTER`.

#search include

`/include<CR>`

That'll light up all the hits.

you can press 'n' to go to the next instance of the result or 'N' to go to the previous one. You can also start by searching backward using '?' instead of '/'.



**jumping to certain characters**

#jump forward and load on the character '<'

`f<`

#jump forward and load right before the character '<'

`t<`

You can think of this as "find" for the first one, which lands right on it, and "to" for the second one, which lands right before it.

So, we can find a certain character, it's a object, We can use any motions on it.

`ct<`, this command is the kind of them.



**a search reference**

`/{string}` search for string

`t` jump up to character

`f` jump onto character

`*` search for other instance of the word under your curser

`n` go to the next instance when you've searched for a string

`N` go to the previous instance when you've searched for a string 

`;` go to the next instance when you've jumped to a character

`,` go to the previous instance when you've jumped to a character



### moving around in your text

Getting around within your text is critical(关键的) to productivity.

**basic motions**

`j` move down one line

`k` move up one line

`h` move left one character

`l` move right one character



**moving within the line**

`o` move to the beginning of the line

`$` move to the end of the line

`^` move to the first non-blank character in the line

`t"` jump to the right before the next quotes

`f"` jump and land on the next quotes



**moving by word**

`w` move forward one word

`b` move back one word

`e` move to the end of your word

when you use uppercase you ignore some delimiters within a string that may break it into two words.

`W` move forward one big word

`B` move back one big word



**moving by sentence or paragraph**

`)` move forward one sentence

`}` move forward one paragraph

`(` move back one sentence

`{` move back one paragraph



**moving within the screen**

`H` move to the top of the screen

`M` move to the midden of the screen

`L` move to the bottom of the screen

`gg` move to the top of the file

`G` move to the bottom of the file

`^U` move up half a screen 

`^D` move down half a screen 

`^F` page down

`^B` page up



**jump back and forth**

`Ctrl-i` jump to your previous navigation location

`Ctrl-o` jump back to where you were



**other motions**

`^E` scroll up one line

`^Y` scroll down one line

`:H` show directory

`:line_number` move to a given line number



### changing text

**understanding mode**

![](C:\Users\gnawgnat\Pictures\vimmode.PNG)



**basic change/insert options**

`i` insert before cursor

`I` insert at the beginning of the line

`a` append after cursor

`A` append at the end of the line

`o` open a new line below the current one

`O` open a new line above the current one

`cm` change whatever you define as a *movement*, eg. a word, or a sentence, or a paragraph.

`C` change the current line from where you're

`r` replace the character under your cursor

`R` replace the character under your cursor, but just keep typing afterwards

`s` substitute from where you are to the next command(noun)

`S` substitute the entire current line



#change inside sentence

`cis`

#go to the beginning of the line and enter insert mode

`I`

#start typing right after the cursor

`a`

#delete the line from where you're and enter insert mode

`C`

#delete the entire line you're on, and enter insert mode

`S`

#change case

`~`

#format the current line

`ga ap`



### deleting text

**basic deletion option**

`x` delete the character under the cursor

`X` delete the character before the cursor

`dm` delete whatever you define as a *movement*, e.g. a word, or a sentence, or a paragraph.

`dd` delete the current line

`dt?` delete from where you are to the ?

`D` delete from where you are to the end of the line

`J` join the current line with the next line



### undo and redo(撤销和重做)

`u` undo your last action

`Ctrl-R` redo the last action



### repeating actions

`.` repeat your last actions

let it combined with visual mode is a good idea.



### copy and paste

`y` yank whatever you select

`yy` yank current line

cutting text is simple. It's the same as deleting

`p` paste whatever you've yank or delete text into buffer

One thing to remember about pasting is that it generally starts right after your cursor

`P` paste the yank text before your cursor position



### Spell checking

Somewhere in your vimrc.

`set spell spelllang=en_us`

**finding misspell world**

`]s` go to the next misspell word

`[s` go to the last misspell word

`z=` when on a misspell word, get some suggestions

`zg` mark a misspell word as correct (save this word to \~/.vim/spell/en-utf-8.add)

`zw` mark a good word as misspell

**add shortcut with fix misspell word**

`nnoremap <leader>f 1z=` (set the shortcut with z= and select the first word)

**taggle spell visuals with \<leader>s**

`nnoremap <leader>s set spell!` switch spell visuals



### Substitution(代替，替换)

`:begin_number_line,end_number_lines/old_word/new_word/g` `%` is global, `/` is a sign character for distinguish other character. So can replaced other sign character

`s-old_word-new_old-g` 







## Advanced

### making things repeatable

`n.` find next search word and re-execute the last command. 

### text objects

**word text objects**

some word-basic objects

`iw` inside word

`aw` around word

#delete around word

`daw` 

**sentence objects**

`is` inside sentence

`as` around sentence

#change inside a sentence

`cis`

**other type objects**

`ip` and `ap` paragraph

`i"` and `a"` double quote

`i'` and `a'` single quote

The same works for a few other types of items, including parenthesis, brackets, braces, and tags (think HTML).(double sign)



### Using visual mode

**enter Visual mode**

`v` character-based

`V` line-based

`Ctrl-V` paragraph-based

**selecting inside containers**

Often time you'll be inside some content that is surrounded on both sides by something, such as `, . ( { [`. 

`vi(` select inside of ()

`vi{` select inside of {}

`vi[` select inside of []

you can also add number to that to select two level out(if you inside them)

`v2i{`



#enter visual character-mode and copy two word

`v2wy` /`vwwy`

#enter visual line-mode and delete two line

`Vjjd` /`v1jd` 

#visual select entire paragraph 

`vip`

#select entire paragraph and paste is down below

`vipyjjp`



### combining visual mode with repetition

it's no work!



### using macros

People think macros are scary. They're really not. They really come down to one thing: recording EVERYTHING you do and then doing it again when you replay. 

`qa` start recording a macro named "a"

`q` stop recording

`@a` play back the macro





### tricks

**remove whitespace from at end of a line**

`%s/s+$//`



**change file type**

`set ft=unix`

`set ft=html`

`set ft=dos`

To show the current filetype, run or put `:set filetype` into your `~/.vimrc`



 



