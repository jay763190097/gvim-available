# gvim-available
# 已经安装的插件
```
auto-pairs
bufexplorer
emmet-vim
javacomplete
nerdtree
tagbar
vim-airline
vim-colorshemes
Vundle.vim
winmanager
```

已经在vim80中放入了ctags.exe

![image](https://github.com/jay763190097/gvim-available/blob/master/QQ%E6%88%AA%E5%9B%BE20161208224117.png)

# 判断操作系统是否是 Windows 还是 Linux 
```
let g:iswindows = 0
let g:islinux = 0
if(has("win32") || has("win64") || has("win95") || has("win16"))
    let g:iswindows = 1
else
    let g:islinux = 1
endif
```

# 判断是终端还是 Gvim 
```
if has("gui_running")
    let g:isGUI = 1
else
    let g:isGUI = 0
endif
```

# 常规设置
```
set nocompatible
set fileencoding=utf-8                            "设置当前文件编码
set fileencodings=utf-8,gb2312,gbk,gb18030     "设置支持打开的文件的编码
set termencoding=utf-8
set fileformat=unix  
set fileformats=unix,dos
set encoding=utf-8
set langmenu=zh_CN.UTF-8
language message zh_CN.UTF-8

if (g:iswindows && g:isGUI)
    "解决菜单乱码
    source $VIMRUNTIME/delmenu.vim
    source $VIMRUNTIME/menu.vim
    "解决consle输出乱码
    language messages zh_CN.utf-8
endif

set nu!
filetype off
"set guifont=Consolas:h13
set guifont=Consolas\ for\ Powerline\ FixedD:h13

set tags=tags;
set autochdir
set hidden

set laststatus=2    " 启动显示状态行(1),总是显示状态行(2)
set number                      " 显示行号
set expandtab                 " 是否在缩进和遇到Tab键时使用空格代替; 使用noexpandtab取消设置
set autoindent                  " 自动缩进
set cindent
set confirm
set smartindent                                       "启用智能对齐方式
set softtabstop=4
set tabstop=4                                         "设置Tab键的宽度，可以更改，如：宽度为2
set shiftwidth=4                                      "换行时自动缩进宽度，可更改（宽度同tabstop）
set smarttab                                          "指定按一次backspace就删除shiftwidth宽度
set foldenable                                        "启用折叠
set foldmethod=manual                         "marker 自动折叠方式  indent 折叠方式   manual   手动折叠
" 常规模式下用空格键来开关光标行所在折叠（注：zR 展开所有折叠，zM 关闭所有折叠）
nnoremap <space> @=((foldclosed(line('.')) < 0) ? 'zc' : 'zo')<CR>
set autoread                                           "当文件在外部被修改，自动更新该文件
set ignorecase                                        "搜索模式里忽略大小写
set smartcase                                         "如果搜索模式包含大写字符，不使用 'ignorecase' 选项，只有在输入搜索模式并且打开 

set showcmd              "在状态栏显示当前输入的命令
set showmode       "显示INSERT NORMAL等

set hlsearch
set incsearch

set paste                       " 支持外部复制(好像不管用)
set clipboard+=unnamed          " 与windows共享剪贴板

set history=99                  " keep 99 lines of command history
set showmatch                   " 显示括号配对情况

" 显示/隐藏菜单栏、工具栏、滚动条，可用 Ctrl + F11 切换
if g:isGUI
    set guioptions-=m
    set guioptions-=T
    set guioptions-=r
    set guioptions-=L
    nmap <silent> <c-F11> :if &guioptions =~# 'm' <Bar>
        \set guioptions-=m <Bar>
        \set guioptions-=T <Bar>
        \set guioptions-=r <Bar>
        \set guioptions-=L <Bar>
    \else <Bar>
        \set guioptions+=m <Bar>
        \set guioptions+=T <Bar>
        \set guioptions+=r <Bar>
        \set guioptions+=L <Bar>
    \endif<CR>
endif
set shortmess=atI               " 去掉启动欢迎界面

set completeopt=preview,menu
set ruler
set cursorline
set autowrite
set magic
set nowrap
set linebreak
set iskeyword+=_,$,@,%,#,-


set backspace=indent,eol,start

set undofile

set mouse=a
set selection=exclusive
set selectmode=mouse,key

" 禁止生成临时文件
set nobackup
set noswapfile

" if has("persistent_undo")
"    set undodir = ~/.undodir/
" endif

"autocmd GUIEnter * simalt ~x   " windows下启动vim最大化
winpos 100 10 
set lines=45 columns=150

if has("autocmd")
  au BufReadPost * if line("'\"") > 1 && line("'\"") <= line("$") | exe "normal! g'\"" | endif
endif

"使用自带补全功能
autocmd FileType python set omnifunc=pythoncomplete#Complete
autocmd FileType javascrīpt set omnifunc=javascrīptcomplete#CompleteJS
autocmd FileType html set omnifunc=htmlcomplete#CompleteTags
autocmd FileType css set omnifunc=csscomplete#CompleteCSS
autocmd FileType xml set omnifunc=xmlcomplete#CompleteTags
autocmd FileType php set omnifunc=phpcomplete#CompletePHP
autocmd FileType c set omnifunc=ccomplete#Complete
```

# 插件安装和设置
```
set rtp+=$VIM/vimfiles/bundle/Vundle.vim/
call vundle#begin('$VIM/vimfiles/bundle/')

 "let Vundle manage Vundle, required
 Plugin 'gmarik/Vundle.vim'

 """"""""vim scripts""""""""""""""""""
 Bundle 'winmanager'

 """"""""git上的插件"""""""""""""""
Bundle 'scrooloose/nerdtree'
Bundle 'bufexplorer'
"Bundle 'taglist'
Bundle 'majutsushi/tagbar'
Bundle 'vim-airline'
Bundle 'jiangmiao/auto-pairs'
Bundle 'mattn/emmet-vim'
Bundle 'javacomplete'


Bundle 'flazz/vim-colorschemes'

call vundle#end()

filetype on                                          "启用文件类型侦测
filetype plugin on                                "针对不同的文件类型加载对应的插件
filetype plugin indent on                     "启用缩进

syntax enable
syntax on

" 设置winmanager
" 设置界面分割
let g:winManagerWindowLayout = "FileExplorer"
"设置winmanager的宽度，默认为25
let g:winManagerWidth = 30
"定义打开关闭winmanager快捷键为F8
nmap <silent> <F8> :WMToggle<cr>
"在进入vim时自动打开winmanager
let g:AutoOpenWinManager = 1

" Tagbar配置
nmap <silent> <F4> :TagbarToggle<CR>
let g:tagbar_ctags_bin = 'ctags'
let g:tagbar_width = 30

" TagList 插件配置 
"nmap tl :TagbarClose<CR>:Tlist<CR>
"let Tlist_Auto_Open=1
"let Tlist_Show_One_File=1                    "只显示当前文件的tags
"let Tlist_Enable_Fold_Column=0              "使taglist插件不显示左边的折叠行
"let Tlist_Exit_OnlyWindow=1                 "如果Taglist窗口是最后一个窗口则退出Vim
"let Tlist_File_Fold_Auto_Close=1               "自动折叠
"let Tlist_WinWidth=30                             "设置窗口宽度
"let Tlist_Use_Right_Window=1                "在右侧窗口中显示

" NERDTree plugin
map <F2> :NERDTreeMirror<CR>
map <F3> :NERDTreeToggle<CR>

" 设置主题
colorscheme freya     

let g:airline_theme="luna" 

"这个是安装字体后 必须设置此项" 
let g:airline_powerline_fonts = 1   

 "打开tabline功能,方便查看Buffer和切换，这个功能比较不错"
 "我还省去了minibufexpl插件，因为我习惯在1个Tab下用多个buffer"
 let g:airline#extensions#tabline#enabled = 1
 let g:airline#extensions#tabline#buffer_nr_show = 1

 "设置切换Buffer快捷键"
 nnoremap <C-Q> :bn<CR>
 nnoremap <C-P> :bp<CR>

 " 关闭状态显示空白符号计数,这个对我用处不大"
 let g:airline#extensions#whitespace#enabled = 0
 let g:airline#extensions#whitespace#symbol = '!'

  if !exists('g:airline_symbols')
    let g:airline_symbols = {}
  endif

  " 箭头图标的显示
  " old vim-powerline symbols
  let g:airline_left_sep = '⮀'
  let g:airline_left_alt_sep = '⮁'
  let g:airline_right_sep = '⮂'
  let g:airline_right_alt_sep = '⮃'
  let g:airline_symbols.branch = '⭠'
  let g:airline_symbols.readonly = '⭤'
  let g:airline_symbols.linenr = '⭡'
```
# emmet配置
```
let g:user_emmet_install_global = 0
let g:user_emmet_settings = {
    \'html' : {
    \    'indent_blockelement': 1
    \}
\}
autocmd FileType html,css,sass,scss,less,php EmmetInstall
```
# javacomplete配置
```
setlocal omnifunc=javacomplete#Complete
autocmd FileType java set omnifunc=javacomplete#Complete
autocmd FileType java set completefunc=javacomplete#CompleteParamsInf
autocmd FileType java inoremap
```
