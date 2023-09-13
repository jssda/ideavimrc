# ideavimrc
" options and mappings that are supported by both Vim and IdeaVim
" 显示行号和相对行号
set number
set relativenumber

" sethandler <C-O> i:ide
" sethandler <C-I> i:ide
" sethandler <C-U> i:ide

" 插件, 设置输入命令时候的输入法插件
set keep-english-in-normal-and-restore-in-insert
" 进入insert模式时根据上下文判断是否恢复输入法，0禁用，1启用
let context_aware=0

" 屏幕滚动时在光标上下方保留5行预览代码
set scrolloff=5
" 屏幕滚动左右保留预览代码行数
set sidescrolloff=5

" 共享系统剪切板
" set clipboard^=unnamedplus,unnamed

" 高亮搜索
set incsearch
set hlsearch

" 映射<C-L>为停止搜索高亮 配置\<SPACE>为停止搜索高亮
nnoremap <silent> <C-L> :nohlsearch<CR>
nnoremap <leader><space> :nohlsearch<CR>

" 显示模式
set showmode

" 配置智能缩进
set smartIndent

" 重构禁用选择模式
" set idearefactormode=keep

" 格式化快捷键配置为Q
map Q gq

"配置 C-a  C-x 快捷键进行加减树的基底, 讲以0为开头的数字默认识别为8进制功能给删除掉
set nrformats-=octal

" 忽略搜索时候的大小写, 可使用\c来进行临时关闭"
"	模式	'ignorecase'  'smartcase'	匹配 ~
" 	foo	  关		-		foo
"	foo	  开		-		foo Foo FOO
"	Foo	  开		关		foo Foo FOO
" 	Foo	  开		开		    Foo
" 	\cfoo	  -		-		foo Foo FOO
" 	foo\C	  -		-		foo
"
set ignorecase
set smartcase

" Toggle case and start typing. E.g. `<leader>iget`: `property` -> `getProperty`
nmap <leader>i ~hi
" Remove selection and toggle case. E.g. `v2l<leader>u`: `getProperty` -> `property`
vmap <leader>u d~h

" 配置使用J字符将两行合并为一行, 即idea中的CTRL-j快捷键的功能
set ideajoin

" 同步idea的书签
set ideamarks

" Use ctrl-c as an ide shortcut in normal and visual modes 配置CTRL-C在普通模式和可视模式中为idea快捷键, 在插入模式为vim快捷键
sethandler <C-C> n-v:ide i:vim

nnoremap <C-S> <ESC>"*p
inoremap <C-S> <ESC>"*p

nnoremap <S-Left> :action EditorLeftWithSelection<CR>
nnoremap <S-Right> :action EditorRightWithSelection<CR>
nnoremap <S-Up> :action EditorUpWithSelection<CR>
nnoremap <S-Down> :action EditorDownWithSelection<CR>

inoremap <S-Left> <C-O>:action EditorLeftWithSelection<CR>
inoremap <S-Right> <C-O>:action EditorRightWithSelection<CR>
inoremap <S-Up> <C-O>:action EditorUpWithSelection<CR>
inoremap <S-Down> <C-O>:action EditorDownWithSelection<CR>

nnoremap g0 ^

""" Plugin
"" 快速移动插件
Plug 'easymotion/vim-easymotion'
map ,, <Plug>(easymotion-prefix)
unmap <C-S-;>

Plug 'tommcdo/vim-exchange' " 交换插件

"" 括号插件
Plug 'tpope/vim-surround'

if has('ide')
    " mapping and options that exist only in IdeaVim
    map <leader>f <Action>(GotoFile)
    map <leader>a <Action>(GotoAction)
    map <leader>b <Action>(Switcher)
    map <leader>i <Action>(ImplementMethods)
    " Map \r to the Reformat Code action
    map <leader>r <Action>(ReformatCode)
    " 展示javaDoc 原idea<C-Q>快捷键
    map <leader>q <Action>(QuickJavaDoc)
    "" 查看方法调用
    nmap <leader>c <Action>(CallHierarchy)
    "" 高亮正在使用的单词
    nmap <leader>h <Action>(HighlightUsagesInFile)
    "" 查看调用情况
    nmap <leader>s <Action>(ShowUsages)
    "" 查看依赖树
    nmap <leader>t <Action>(TypeHierarchy)
    "" 查询谁在使用
    nmap <leader>u <Action>(FindUsages)
    "" 集中焦点到编辑器
    nmap <leader>x <Action>(HideAllWindows)

    "" 方法跳跃
    nmap [[ <Action>(MethodUp)
    nmap ]] <Action>(MethodDown)

    "" 跳转到声明
    nmap gD <Action>(GotoTypeDeclaration)

  if &ide =~? 'intellij idea'
    if &ide =~? 'community'
      " some mappings and options for IntelliJ IDEA Community Edition
    elseif &ide =~? 'ultimate'
      " some mappings and options for IntelliJ IDEA Ultimate Edition
    endif
  elseif &ide =~? 'pycharm'
    " PyCharm specific mappings and options
  endif
else
  " some mappings for Vim/Neovim
  nnoremap <leader>f <cmd>Telescope find_files<cr>
endif
