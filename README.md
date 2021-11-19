# nvim
----------------------

include install process and some tools

## **pre install**

---------------

**neovim pre install**

pip install pynvim(pip install neovim)

pacman -S nodejs

npm install -g neovim

**tools pre install**

pip install debugpy(python程序调试,通过vimspector实现)

pacman -S xclip

*xclip 是一个命令行实用程序，设计用于运行在任何有X11实现的系统上。它提供了一个从命令行到X selection(“剪贴板”)的接口。它可以从标准输入或文件中读取数据，并将其放在X selection中，以便粘贴到其他应用程序中。xclip还可以将X selection打印到标准输出，然后将其重定向到一个文件或另一个程序。*

pacman -S install ctags

*ctags 获得类/函数/变量的三重支持*

pacman -S fzf

pacman -S ranger

ranger --copy-config=all

pacman -S the_silver_searcher(silversearcher-ag)

*ag 是一个全文检索工具，非常适合查询大量文本文件，或者源代码的场景。常用的一个方式便是在目录中搜索关键词，ag能够非常快速的搜索文件内容，所以非常适合查询日志，或者代码等文本文件。唯一发现的缺点就是想要搜索中文内容时，发现ag并不能很好的处理。*

**about language-server** 

coc-settings.json在coc自动补全中用到的language-server需要安装

pacman -S ccls,pacman -S bash-language-server


## using tools
### Markdown
#### vim-instant-markdown

Plug 'suan/vim-instant-markdown', {'for': 'markdown'}

npm install install-markdown-d

#### md-snippets

定义一些markdown快捷键(md-snippets.vim)

#### vimwiki

管理markdown文件

leader ww

### coc
`set hidden` 　

+ 缓冲区未保存可以跳到其他地方

`set updatetime = 100` 

+ 响应时间更快

`set shortmess+=c` 

+ 省略自动补全是匹配的第几个信息
```
inoremap <silent><expr> <TAB>

	\ pumvisible() ? "\<C-n>" :
	\ <SID>check_back_space() ? "\<TAB>" :
	\ coc#refresh()
inoremap <expr><S-TAB> pumvisible() ? "\<C-p>" : "\<C-h>"

function! s:check_back_space() abort
	let col = col('.') - 1
	return !col || getline('.')[col - 1]  =~# '\s'
endfunction
```
+ 使得TAB键弹出补全

`inoremap <silent><expr> <c-o> coc#refresh()`

+ 使用ctrl+o 没有前面的内容就弹出补全提示

```
inoremap <silent><expr> <cr> pumvisible() ? coc#_select_confirm()
                              \: "\<C-g>u\<CR>\<c-r>=coc#on_enter()\<CR>"
```
+ 使用TAB选中补全后，回车不换行
```
function! Show_documentation()
	call CocActionAsync('highlight')
	if (index(['vim','help'], &filetype) >= 0)
		execute 'h '.expand('<cword>')
	else
		call CocAction('doHover')
	endif
endfunction

nnoremap <LEADER>h :call Show_documentation()<CR>
```
+ leader+h 调出帮助文档
```
nmap <silent> <leader>- <Plug>(coc-diagnostic-prev)
nmap <silent> <leader>= <Plug>(coc-diagnostic-next)	
```
+ 使用leader+-或=跳转到上个或下个报错的地方

`nnoremap <silent><nowait> <LEADER>d :CocList diagnostics<cr> `

+ 使用leader+d列出所有报错

```
nmap <silent> gd <Plug>(coc-definition) 查看函数定义

nmap <silent> gy <Plug>(coc-type-definition)

nmap <silent> gi <Plug>(coc-implementation)

nmap <silent> gr <Plug>(coc-references) 查看函数引用

nmap <leader>rn <Plug>(coc-rename)  leader+rn函数内变量统一改名
 
xmap <leader>a  <Plug>(coc-codeaction-selected)
nmap <leader>a  <Plug>(coc-codeaction-selected)

nnoremap <silent> <space>y :<C-u>CocList -A --normal yank<cr>  space+y打开剪切板历史
```


#### coc-snippets 
snippets preview requires neovim 0.4 or latest vim8

detail as [coc-snippets](https://github.com/neoclide/coc-snippets)

```
" coc-snippets
imap <C-l> <Plug>(coc-snippets-expand)
vmap <C-e> <Plug>(coc-snippets-select)
let g:coc_snippet_next = '<c-e>'
let g:coc_snippet_prev = '<c-n>'
imap <C-e> <Plug>(coc-snippets-expand-jump)
let g:snips_author = 'theniceboy'
autocmd BufRead,BufNewFile tsconfig.json set filetype=jsonc
autocmd FileType python let b:coc_root_patterns = ['.git', '.env', 'venv', '.venv', 'setup.cfg', 'setup.py', 'pyproject.toml', 'pyrightconfig.json']
```





### Ultisnips



### nerd-commmentator

批注/反批注

### vimf-surround

修改包裹符号

### switch
快捷修改true,false

### tabgularize

规整代码(等号)

### simgplyfold
把代码收起来

#tag bar
shift+T:列出代码函数和变量

### vim-signature
为代码添加书签

#undotree
当前文件的编辑历史

### fzf 
trl p :查找文件 
ctrl o 回到上一个文件 
ctrl i 回到新打开的文件
