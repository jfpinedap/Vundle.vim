## [Help Maintain Vundle](https://github.com/VundleVim/Vundle.vim/issues/383)

## Table of Contents

- [About](#about)
- [Quick Start](#quick-start)
- [Docs](#docs)
- [Changelog](#changelog)
- [People Using Vundle](#people-using-vundle)
- [Contributors](#contributors)
- [Inspiration & Ideas](#inspiration--ideas)
- [Also](#also)
- [TODO](#todo)

## About

[Vundle] is short for _Vim bundle_ and is a [Vim] plugin manager.

[Vundle] allows you to...

* keep track of and [configure] your plugins right in the `.vimrc`
* [install] configured plugins (a.k.a. scripts/bundle)
* [update] configured plugins
* [search] by name all available [Vim scripts]
* [clean] unused plugins up
* run the above actions in a *single keypress* with [interactive mode]

[Vundle] automatically...

* manages the [runtime path] of your installed scripts
* regenerates [help tags] after installing and updating

[Vundle] is undergoing an [interface change], please stay up to date to get latest changes.

[![Gitter-chat](https://badges.gitter.im/VundleVim/Vundle.vim.svg)](https://gitter.im/VundleVim/Vundle.vim) for discussion and support.

![Vundle-installer](http://i.imgur.com/Rueh7Cc.png)

## Quick Start

1. Introduction:

   Installation requires [Git] and triggers [`git clone`] for each configured repository to `~/.vim/bundle/` by default.
   Curl is required for search.

   If you are using Windows, go directly to [Windows setup]. If you run into any issues, please consult the [FAQ].
   See [Tips] for some advanced configurations.

   Using non-POSIX shells, such as the popular Fish shell, requires additional setup. Please check the [FAQ].

2. Set up [Vundle]:

   ` git clone https://github.com/VundleVim/Vundle.vim.git ~/.vim/bundle/Vundle.vim`

3. Configure Plugins:

   Put this at the top of your `.vimrc` to use Vundle. Remove plugins you don't need, they are for illustration purposes.

   ```vim
   " jfpinedap setings for https://github.com/VundleVim/Vundle.vim  
set nocompatible  " be iMproved, required
filetype off  " required
set exrc

set rtp+=~/.vim/bundle/Vundle.vim
call vundle#begin()

" ==== Icons
Plugin 'ryanoasis/vim-devicons'

" ==== plugin manager
Plugin 'VundleVim/Vundle.vim'

" ==== helpers
Plugin 'vim-scripts/L9'

" ==== File tree
Plugin 'scrooloose/nerdtree'

" ==== Completion
Plugin 'Valloric/YouCompleteMe'

" ==== Git
Plugin 'airblade/vim-gitgutter'
Plugin 'tpope/vim-fugitive'

" ==== syntax helpers
Plugin 'scrooloose/syntastic'
Plugin 'tpope/vim-surround'
Plugin 'cakebaker/scss-syntax.vim'
Plugin 'othree/yajs.vim'
Plugin 'mitsuhiko/vim-jinja'
Plugin 'octol/vim-cpp-enhanced-highlight'
Plugin 'ap/vim-css-color'
Plugin 'Vimjas/vim-python-pep8-indent'

" ==== moving / searching
Plugin 'easymotion/vim-easymotion'
Plugin 'kien/ctrlp.vim'

" ==== snippets
Plugin 'SirVer/ultisnips'

" Status bar on bottom
Plugin 'bling/vim-airline'

" ==== PLUGIN THEMES
Plugin 'morhetz/gruvbox'

call vundle#end()
filetype plugin indent on

" ==== Colors and other basic settings
colorscheme gruvbox
set guifont=Monospace\ 11
set fillchars+=vert:'
syntax enable
set background=dark
set ruler
"set hidden "Don't show The message --> E37: No write since last change (add ! to override)
" and if opening a new file when the current buffer has unsaved changes causes files to be hidden instead of closed
set number
set laststatus=2
set smartindent
set st=4 sw=4 et
set tabstop=4     " The width of a TAB is set to 4. Still it is a \t. It is just that Vim will interpret it to be having a width of 4.                
set softtabstop=4 " Sets the number of columns for a TAB.
set expandtab     " Expand TABs to spaces.
set shiftwidth=4  " Indents will have a width of 4.
set smarttab

"let &colorcolumn="80"
:set guioptions-=m  "remove menu bar
:set guioptions-=T  "remove toolbar
:set guioptions-=r  "remove right-hand scroll bar
:set guioptions-=L  "remove left-hand scroll bar
":set lines=999 columns=999

" ==== NERDTREE
let NERDTreeIgnore = ['__pycache__', '\.pyc$', '\.o$', '\.so$', '\.a$', '\.swp', '*\.swp', '\.swo', '\.swn', '\.swh', '\.swm', '\.swl', '\.swk', '\.sw*$', '[a-zA-Z]*egg[a-zA-Z]*', '.DS_Store']

let NERDTreeShowHidden=1
let g:NERDTreeWinPos="left"
let g:NERDTreeDirArrows=0
map <C-t> :NERDTreeToggle<CR>
silent! map <F3> :NERDTreeFind<CR>
"let g:NERDTreeMapActivateNode="<F3>"
"let g:NERDTreeMapPreview="<F4>"

" ==== Syntastic
let g:syntastic_always_populate_loc_list = 1
let g:syntastic_auto_loc_list = 1
let g:syntastic_check_on_open = 1
let g:syntastic_check_on_wq = 0
set statusline+=%#warningmsg#
set statusline+=%{SyntasticStatuslineFlag()}
set statusline+=%*
let g:syntastic_javascript_checkers = ['eslint']
let g:syntastic_javascript_mri_args = "--config=$HOME/.jshintrc"
let g:syntastic_python_checkers = [ 'pylint', 'flake8', 'pep8', 'pyflakes', 'python']
let g:syntastic_yaml_checkers = ['jsyaml']
let g:syntastic_html_tidy_exec = 'tidy5'

" === flake8
let g:flake8_show_in_file=1

" ==== snippets
let g:UltiSnipsExpandTrigger="<A-ENTER>"
let g:UltiSnipsJumpForwardTrigger="<A-ENTER>"
let g:UltiSnipsJumpBackwardTrigger="<A-BACKSPACE>"
" If you want :UltiSnipsEdit to split your window.
let g:UltiSnipsEditSplit="vertical"

" ==== Easymotion
let g:EasyMotion_do_mapping = 0
let g:EasyMotion_smartcase = 1
nmap f <Plug>(easymotion-s)

" ==== moving around
nmap <silent> <C-k> :wincmd k<CR>
nmap <silent> <C-j> :wincmd j<CR>
nmap <silent> <C-h> :wincmd h<CR>
nmap <silent> <C-l> :wincmd l<CR>
"nmap <silent> <A-Up> :wincmd k<CR>
"nmap <silent> <A-Down> :wincmd j<CR>
"nmap <silent> <A-Left> :wincmd h<CR>
"nmap <silent> <A-Right> :wincmd l<CR>

" ==== disable mouse
"set mouse=c

" ==== disable swap file warning
"set shortmess+=A

" ==== custom commands
command JsonPretty execute ":%!python -m json.tool"
set secure

"execute pathogen#infect()
set ttymouse=xterm2
set mouse=a
set number
syntax on
inoremap <C-v> <ESC>"+pa
vnoremap <C-c> "+y
"vnoremap <C-d> "+d
"filetype plugin indent on
"autocmd vimenter * NERDTree "uncomment if you what to open a NERDTree automatically when vim starts up

   ```

4. Install Plugins:

   Launch `vim` and run `:PluginInstall`

   To install from command line: `vim +PluginInstall +qall`

5. (optional) For those using the fish shell: add `set shell=/bin/bash` to your `.vimrc`

## Docs

See the [`:h vundle`](https://github.com/VundleVim/Vundle.vim/blob/master/doc/vundle.txt) Vimdoc for more details.

## Changelog

See the [changelog](https://github.com/VundleVim/Vundle.vim/blob/master/changelog.md).

## People Using Vundle

see [Examples](https://github.com/VundleVim/Vundle.vim/wiki/Examples)

## Contributors

see [Vundle contributors](https://github.com/VundleVim/Vundle.vim/graphs/contributors)

*Thank you!*

## Inspiration & Ideas

* [pathogen.vim](http://github.com/tpope/vim-pathogen/)
* [Bundler](https://github.com/bundler/bundler)
* [Scott Bronson](http://github.com/bronson)

## Also

* Vundle was developed and tested with [Vim] 7.3 on OS X, Linux and Windows
* Vundle tries to be as [KISS](http://en.wikipedia.org/wiki/KISS_principle) as possible

## TODO
[Vundle] is a work in progress, so any ideas and patches are appreciated.

* [x] activate newly added bundles on `.vimrc` reload or after `:PluginInstall`
* [x] use preview window for search results
* [x] Vim documentation
* [x] put Vundle in `bundles/` too (will fix Vundle help)
* [x] tests
* [x] improve error handling
* [ ] allow specifying revision/version?
* [ ] handle dependencies
* [ ] show description in search results
* [ ] search by description as well
* [ ] make it rock!

[Vundle]:http://github.com/VundleVim/Vundle.vim
[Windows setup]:https://github.com/VundleVim/Vundle.vim/wiki/Vundle-for-Windows
[FAQ]:https://github.com/VundleVim/Vundle.vim/wiki
[Tips]:https://github.com/VundleVim/Vundle.vim/wiki/Tips-and-Tricks
[Vim]:http://www.vim.org
[Git]:http://git-scm.com
[`git clone`]:http://gitref.org/creating/#clone

[Vim scripts]:http://vim-scripts.org/vim/scripts.html
[help tags]:http://vimdoc.sourceforge.net/htmldoc/helphelp.html#:helptags
[runtime path]:http://vimdoc.sourceforge.net/htmldoc/options.html#%27runtimepath%27

[configure]:https://github.com/VundleVim/Vundle.vim/blob/v0.10.2/doc/vundle.txt#L126-L233
[install]:https://github.com/VundleVim/Vundle.vim/blob/v0.10.2/doc/vundle.txt#L234-L254
[update]:https://github.com/VundleVim/Vundle.vim/blob/v0.10.2/doc/vundle.txt#L255-L265
[search]:https://github.com/VundleVim/Vundle.vim/blob/v0.10.2/doc/vundle.txt#L266-L295
[clean]:https://github.com/VundleVim/Vundle.vim/blob/v0.10.2/doc/vundle.txt#L303-L318
[interactive mode]:https://github.com/VundleVim/Vundle.vim/blob/v0.10.2/doc/vundle.txt#L319-L360
[interface change]:https://github.com/VundleVim/Vundle.vim/blob/v0.10.2/doc/vundle.txt#L372-L396
