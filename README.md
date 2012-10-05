# Vim as IDE

## Steps to clone and setup this vim-config

	cd ~
	git clone git://github.com/pixelhandler/vim-config.git ./.vim
    cd ~/.vim
    git submodule init
    git submodule update
    git submodule foreach git submodule init
    git submodule foreach git submodule update
    cd ~/.vim/bundle/command-t/
    rake make --ruby=/usr/bin/ruby
    mkdir ~/.vim/_backup
    mkdir ~/.vim/_temp
    ln -s ~/.vim/.vimrc ~/.vimrc
    cd ~

*Note: for vagrant users I added a shell script you can use with your provision script, see the vagrant-vim.sh file*

## Steps used create this vim-config repository…

1. Initialize the repo
2. Add submodules
3. Setup pathogen
4. Initialize bundle(s), e.g. command-t
5. Create a .vimrc file
6. Use a symbolic link to .vimrc in my home directory

### 1. Intitials the repo

	mkdir ~/.vim/
	mkdir ~/.vim/{autoload,bundle}
	cd ~/.vim/
	git init

### 2. Add submodules

	git submodule add http://github.com/tpope/vim-fugitive.git bundle/fugitive
	git submodule add https://github.com/msanders/snipmate.vim.git bundle/snipmate
	git submodule add https://github.com/tpope/vim-surround.git bundle/surround
	git submodule add https://github.com/tpope/vim-git.git bundle/git
	git submodule add https://github.com/ervandew/supertab.git bundle/supertab
	git submodule add https://github.com/wincent/Command-T.git bundle/command-t
	git submodule add https://github.com/fholgado/minibufexpl.vim.git bundle/minibufexpl
	git submodule add https://github.com/mileszs/ack.vim.git bundle/ack
	git submodule add https://github.com/sjl/gundo.vim.git bundle/gundo
	git submodule add https://github.com/vim-scripts/TaskList.vim.git bundle/tasklist
	git submodule add https://github.com/vim-scripts/The-NERD-tree.git bundle/nerdtree
	git submodule add https://github.com/mattn/zencoding-vim.git bundle/zencoding
	git submodule add https://github.com/hallettj/jslint.vim.git bundle/jslint
	git submodule add https://github.com/walm/jshint.vim.git bundle/jshint
	git submodule add https://github.com/scrooloose/nerdcommenter.git bundle/nerdcommenter
	git submodule add https://github.com/spf13/PIV.git bundle/PIV
	git submodule add https://github.com/groenewege/vim-less.git bundle/less
	git submodule add https://github.com/vim-scripts/matchindent.vim.git bundle/matchindent
	git submodule add https://github.com/tpope/vim-markdown.git bundle/markdown
	git submodule add https://github.com/godlygeek/tabular.git bundle/tabular
    git submodule add https://github.com/scrooloose/syntastic.git bundle/syntastic

	git submodule add https://github.com/vim-scripts/peaksea.git bundle/peaksea
	git submodule add https://github.com/yearofmoo/Vim-Darkmate.git bundle/darkmate/colors
	git submodule add https://github.com/gilesbowkett/ir_black.git bundle/ir_black/colors
	git submodule add https://github.com/altercation/vim-colors-solarized.git bundle/solarized
	git submodule add https://github.com/marcus/vim-mustang.git bundle/mustang
	git submodule add https://github.com/therubymug/vim-pyte.git bundle/pyte
	git submodule add https://github.com/vim-scripts/mayansmoke.git bundle/mayansmoke
	git submodule add https://github.com/w0ng/vim-hybrid.git bundle/hybrid
	
	git submodule init
	git submodule update
	git submodule foreach git submodule init
	git submodule foreach git submodule update

### 3. Setup pathogen

pathogen.vim Install to `~/.vim/autoload/pathogen.vim`

	curl -so ~/.vim/autoload/pathogen.vim https://raw.github.com/tpope/vim-pathogen/master/autoload/pathogen.vim

Must haves in my .vimrc to use pathogen:

	filetype off
	call pathogen#runtime_append_all_bundles()
	call pathogen#helptags()

### 4. Initialize bundle: command-t
	
	cd bundle/command-t/
	rake make

### 5. Create a .vimrc file

	" ----------------------------------------------------------
	" Use Vim settings, rather then Vi settings (much better!).
	" This must be first, because it changes other options as a side effect.
	set nocompatible      " Use vim, no vi defaults
	
	
	" ----------------------------------------------------------
	" Pathogen Initialization
	
	" This loads all the plugins in ~/.vim/bundle
	" Use tpope's pathogen plugin to manage all other plugins
	
	" Filetype detection must be off when you run the commands
	filetype off
	call pathogen#runtime_append_all_bundles()
	"call pathogen#infect()
	call pathogen#helptags()
	
	
	" ----------------------------------------------------------
	" Git
	
	" Integration with Git, perhaps add to status line %{fugitive#statusline()}
	" Fugitive commands...
	" Gblame: This allows you to view a line by line comparison of who the last person to touch that line of code is.
	" Gwrite: This will stage your file for commit, basically doing git add <filename>
	" Gread: This will basically run a git checkout <filename>
	" Gcommit: This will just run git commit. Since its in a vim buffer, you can use keyword completion (Ctrl-N), like test_all<Ctrl-N> to find the method name in your buffer and complete it for the commit message. You can also use + and - on the filenames in the message to stage/unstage them for the commit.
	
	
	" ----------------------------------------------------------
	" Tab Completion and Documentation
	
	let g:SuperTabDefaultCompletionType = "context"
	set completeopt=menuone,longest,preview
	
	
	" Code Navigation
	" Buffers, minibufexpl plugin
	" You can switch between the buffers using b<number>, such as :b1 for the first buffer. 
	" You can also use its name to match, so you can type :b mod<tab>
	" To close a buffer you use :bd or :bw.
	
	
	" ----------------------------------------------------------
	" Mappings and bundle settings
	
	" Graph your Vim undo tree in style, gundo.vim
	nnoremap <F5> :GundoToggle<CR>
	
	" Task lists, TaskList.vim
	map <leader>td <Plug>TaskList
	
	" Gundo plugin
	map <leader>g :GundoToggle<CR>
	
	" File Browser, NERDTree
	map <leader>n :NERDTreeToggle<CR>
	let NERDTreeShowHidden=1
	
	" Searching, Ack
	nmap <leader>a <Esc>:Ack!
	
	" Window Splits, bind Ctrl+<movement> keys to move around the windows, 
	" instead of using Ctrl+w + <movement>:
	map <c-j> <c-w>j
	map <c-k> <c-w>k
	map <c-l> <c-w>l
	map <c-h> <c-w>h
	
	" use :w!! to write to a file using sudo if you forgot to 'sudo vim file'
	" (it will prompt for sudo password when writing)
	cmap w!! %!sudo tee > /dev/null %
	
	map <C-\> :tnext<CR>
	" Opens an edit command with the path of the currently edited file filled in
	" Normal mode: <Leader>e
	map <Leader>e :e <C-R>=expand("%:p:h") . "/" <CR>
	
	" Opens a tab edit command with the path of the currently edited file filled in
	" Normal mode: <Leader>t
	map <Leader>te :tabe <C-R>=expand("%:p:h") . "/" <CR>
	
	" Shortcut to rapidly toggle `set list`
	nmap <leader>l :set list!<CR>
	
	" cd to the directory containing the file in the buffer
	nmap <silent> <leader>cd :lcd %:h<CR>
	
	" Create the directory containing the file in the buffer
	nmap <silent> <leader>md :!mkdir -p %:p:h<CR>
	
	" Some helpers to edit mode
	" http://vimcasts.org/e/14
	cnoremap %% <C-R>=expand('%:h').'/'<cr>
	map <leader>ew :e %%
	map <leader>es :sp %%
	map <leader>ev :vsp %%
	map <leader>et :tabe %%
	
	" format the entire file
	nmap <leader>fef ggVG=
	
	" upper/lower word
	nmap <leader>u mQviwU`Q
	nmap <leader>l mQviwu`Q
	
	" upper/lower first char of word
	nmap <leader>U mQgewvU`Q
	nmap <leader>L mQgewvu`Q
	
	" find merge conflict markers
	nmap <silent> <leader>fc <ESC>/\v^[<=>]{7}( .*\|$)<CR>
	
	" Map command-[ and command-] to indenting or outdenting
	" while keeping the original selection in visual mode
	vmap <A-]> >gv
	vmap <A-[> <gv
	
	nmap <A-]> >>
	nmap <A-[> <<
	
	omap <A-]> >>
	omap <A-[> <<
	
	imap <A-]> <Esc>>>i
	imap <A-[> <Esc><<i
	
	" Map Control-# to switch tabs
	map  <C-0> 0gt
	imap <C-0> <Esc>0gt
	map  <C-1> 1gt
	imap <C-1> <Esc>1gt
	map  <C-2> 2gt
	imap <C-2> <Esc>2gt
	map  <C-3> 3gt
	imap <C-3> <Esc>3gt
	map  <C-4> 4gt
	imap <C-4> <Esc>4gt
	map  <C-5> 5gt
	imap <C-5> <Esc>5gt
	map  <C-6> 6gt
	imap <C-6> <Esc>6gt
	map  <C-7> 7gt
	imap <C-7> <Esc>7gt
	map  <C-8> 8gt
	imap <C-8> <Esc>8gt
	map  <C-9> 9gt
	imap <C-9> <Esc>9gt
	
	
	" ----------------------------------------------------------
	" Backup and swap files
	
	set backupdir=~/.vim/_backup//  " where to put backup files.
	set directory=~/.vim/_temp//    " where to put swap files.
	
	
	" ----------------------------------------------------------
	" General Config
	
	set encoding=utf-8              "Set default encoding to UTF-8
	
	set number                      "Line numbers are good
	set ruler                       "Show line and column number
	set backspace=indent,eol,start  "Allow backspace in insert mode
	set history=1000                "Store lots of :cmdline history
	set showcmd                     "Show incomplete cmds down the bottom
	set showmode                    "Show current mode down the bottom
	set gcr=a:blinkon0              "Disable cursor blink
	set visualbell                  "No sounds
	set autoread                    "Reload files changed outside vim
	
	" This makes vim act like all other editors, buffers can
	" exist in the background without being in a window.
	" http://items.sjbach.com/319/configuring-vim-right
	set hidden
	
	
	" ----------------------------------------------------------
	" White Space
	
	" Indentation
	set autoindent
	set smartindent
	set smarttab
	set shiftwidth=4
	set softtabstop=4
	set tabstop=4
	set expandtab
	
	filetype plugin on
	filetype indent on
	
	" Display tabs and trailing spaces visually
	set list listchars=tab:\ \ ,trail:·
	
	set nowrap       "Don't wrap lines
	set linebreak    "Wrap lines at convenient points
	set list listchars=tab:▸\ ,trail:·
	
	
	" Set tabstop, softtabstop and shiftwidth to the same value
	command! -nargs=* Stab call Stab()
	function! Stab()
	  let l:tabstop = 1 * input('set tabstop = softtabstop = shiftwidth = ')
	  if l:tabstop > 0
	    let &l:sts = l:tabstop
	    let &l:ts = l:tabstop
	    let &l:sw = l:tabstop
	  endif
	  call SummarizeTabs()
	endfunction
	
	function! SummarizeTabs()
	  try
	    echohl ModeMsg
	    echon 'tabstop='.&l:ts
	    echon ' shiftwidth='.&l:SW
	    echon ' softtabstop='.&l:sts
	    if &l:et
	      echon ' expandtab'
	    else
	      echon ' noexpandtab'
	    endif
	  finally
	    echohl None
	  endtry
	endfunction
	
	" Some file types should wrap their text
	function! s:setupWrapping()
	  set wrap
	  set linebreak
	  set textwidth=72
	  set nolist
	endfunction
	
	" Tab completion
	set wildmode=list:longest,list:full
	set wildignore+=*.o,*.obj,.git,*.rbc,*.class,.svn,vendor/gems/*
	
	
	" ----------------------------------------------------------
	" Folds
	
	set foldmethod=indent   "Fold based on indent
	set foldnestmax=3       "Deepest fold is 3 levels
	set nofoldenable        "Don't fold by default
	
	
	
	" ----------------------------------------------------------
	" Syntax Highlighting and Validation
	
	"syntax on                   " syntax highlighing
	syntax enable               " Turn on syntax highlighting allowing local overrides
	
	filetype on                 " try to detect filetypes
	filetype plugin indent on   " enable loading indent file for filetype
	
	" PHP highlighting extras
	" https://github.com/Apreche/vim/blob/master/vimrc
	let php_sql_query = 1
	let php_htmlInStrings = 1
	let php_baselib = 1
	let php_noShortTags=1
	" let php_folding=1
	
	"warning when going over 79 characters per line
	highlight OverLength ctermbg=red ctermfg=white guibg=#592929
	match OverLength /\%80v.*/
	
	
	" Only do this part when compiled with support for autocommands
	if has("autocmd")
	  " Enable file type detection
	  filetype on
	  
	  " In Makefiles, use real tabs, not tabs expanded to spaces
	  autocmd FileType make setlocal noexpandtab
	  
	  " Make sure all markdown files have the correct filetype set and setup wrapping
	  autocmd BufRead,BufNewFile *.{md,markdown,mdown,mkd,mkdn,txt} setf markdown | call s:setupWrapping()
	
	  " Syntax of these languages is fussy over tabs Vs spaces
	  autocmd FileType make setlocal ts=8 sts=8 sw=8 noexpandtab
	  autocmd FileType yaml setlocal ts=2 sts=2 sw=2 expandtab
	
	  " Customisations based on house-style (arbitrary)
	  autocmd FileType html setlocal ts=4 sts=4 sw=4 expandtab
	  autocmd FileType css setlocal ts=4 sts=4 sw=4 expandtab
	  autocmd FileType less setlocal ts=4 sts=4 sw=4 expandtab
	  autocmd FileType javascript setlocal ts=4 sts=4 sw=4 expandtab
	
	  autocmd FileType php setlocal noexpandtab ts=4 sts=4 sw=4
	  autocmd FileType php let g:syntastic_enable_highlighting=0
	  autocmd FileType php let g:syntastic_quiet_warnings=1
	
	  autocmd BufNewFile,BufRead *.json setfiletype javascript
	  autocmd BufNewFile,BufRead *.php setfiletype php
	  autocmd BufNewFile,BufRead *.phtml setfiletype html
	
	  " Treat .rss files as XML
	  autocmd BufNewFile,BufRead *.rss,*.atom setfiletype xml
	
	  " Treat .less files
	  "autocmd BufNewFile,BufRead *.less setfiletype less "setf less
	endif
	
	
	" Turn on jslint errors by default, 0 to disable
	let g:JSLintHighlightErrorLine = 0
	
	
	" ----------------------------------------------------------
	" Colors
	" to find a new color scheme just go to http://code.google.com/p/vimcolorschemetest/
	
	set background=dark
	" set background=light
	
	colorscheme darkmate
	
	" Hybrid
	let g:hybrid_use_Xresources = 1
	" colorscheme hybrid
	
	" colorscheme ir_black
	" colorscheme mayansmoke
	" colorscheme mustang
	" colorscheme peaksea
	" colorscheme pyte
	
	" Solarized
	" colorscheme solarized
	" let g:solarized_termtrans=1
	" let g:solarized_degrade=0
	" let g:solarized_bold=1
	" let g:solarized_underline=1
	" let g:solarized_italic=1
	" let g:solarized_termcolors=256
	" let g:solarized_diffmode="normal"
	" let g:solarized_hitrail=0
	" let g:solarized_menu=1
	" let g:solarized_contrast="high"    "default value is normal
	" let g:solarized_visibility="high"    "default value is normal
	
	
	" ----------------------------------------------------------
	" Status bar
	
	if has("statusline") && !&cp
	  set laststatus=2  " always show the status bar
	
	  " Start the status line
	  set statusline=%f\ %m\ %r
	  set statusline+=Line:%l/%L[%p%%]
	  set statusline+=Col:%v
	  set statusline+=Buf:#%n
	  set statusline+=[%b][0x%B]
	endif
	
	" Show (partial) command in the status line
	set showcmd


### 6. Use a symbolic link to .vimrc

	ln -s ~/.vim/.vimrc ~/.vimrc

## References
 
* <http://sontek.net/blog/detail/turning-vim-into-a-modern-python-ide>
* <https://github.com/carlhuda/janus/>