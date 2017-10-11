// vim 配置文件留存
```vim?linenums
set number
set go=
color darkblue
"set guifont=Source\ Code\ Pro:h10.5:cANSI
set guifont=Mononoki:h12
winpos 100 100
set ruler
set showcmd
set foldenable
syntax on
set nobackup
set clipboard+=unnamed
"set autoindent
set cindent
set tabstop=2
set softtabstop=2
set shiftwidth=2
set smarttab
set ignorecase
set backspace=2
set showmatch
set scrolloff=3
set guioptions+=m
set expandtab
set lines=40
set columns=80
set noerrorbells

"## KBD-map
"=========================================================================

set winaltkeys=no " Or <A-xxx> maynot work as your image

"### Auto complete
"inoremap ( ()<ESC>i
"inoremap [ []<ESC>i
inoremap { {}<ESC>i
"inoremap < <><ESC>i
"inoremap " ""<ESC>i
"inoremap ' ''<ESC>i

"### Tabs
noremap <C-n> <ESC>:tabnew<CR>
noremap <C-Tab> <ESC>:tabnext<CR>
noremap <C-S-Tab> <ESC>:tabNext<CR>

"### Normal Mode: cursor move
nnoremap w k
nnoremap s j
nnoremap a h
nnoremap d l
nnoremap ] $
nnoremap [ ^

"### Insert Mode: cursor move
inoremap ; ;<ESC>==$i<Right>
inoremap <A-w> <Up>
inoremap <A-s> <Down>
inoremap <A-a> <Left>
inoremap <A-d> <Right>
inoremap <A-]> <ESC>$i<Right>
inoremap <A-[> <ESC>^i

"### Visual Mode: cursor move
vnoremap w k
vnoremap s j
vnoremap a h
vnoremap d l

"### Normal Mode:
nnoremap <CR> $i<Right><CR><ESC>
```
