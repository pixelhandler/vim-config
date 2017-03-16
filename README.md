# Vim as IDE

## Steps to clone and setup this vim-config

	cd ~
	git clone git://github.com/pixelhandler/vim-config.git ./.vim
    cd ~/.vim
    git submodule init
    git submodule update
    git submodule foreach git submodule init
    git submodule foreach git submodule update
    mkdir ~/.vim/_backup
    mkdir ~/.vim/_temp
    ln -s ~/.vim/.vimrc ~/.vimrc
    cd ~

*Note: for vagrant users I added a shell script you can use with your provision script, see the vagrant-vim.sh file*

## Steps used create this vim-config repository…

1. Setup the repo
2. Add submodules
3. Setup pathogen
4. Create a .vimrc file
5. Use a symbolic link to .vimrc in my home directory

### 1. Setup the repo

	mkdir ~/.vim/
	mkdir ~/.vim/{autoload,bundle}
	cd ~/.vim/
	git init

### 2. Add submodules

	git submodule add http://github.com/tpope/vim-fugitive.git bundle/fugitive

Add some colors

	git submodule add https://github.com/w0ng/vim-hybrid.git bundle/hybrid

Initialize and update

	git submodule init
	git submodule update
	git submodule foreach git submodule init
	git submodule foreach git submodule update

- *[neocomplete]* requires lua support, install vim with lua:

	brew install vim --with-lua

[neocomplete]: https://github.com/Shougo/neocomplete.vim

### 3. Setup pathogen

pathogen.vim Install to `~/.vim/autoload/pathogen.vim`

	curl -so ~/.vim/autoload/pathogen.vim https://raw.github.com/tpope/vim-pathogen/master/autoload/pathogen.vim

Must haves in my .vimrc to use pathogen:

	filetype off
	call pathogen#runtime_append_all_bundles()
	call pathogen#helptags()

### 4. Create a .vimrc file

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

	"… and so on, see the .vimrc file in this repo


### 5. Use a symbolic link to .vimrc

	ln -s ~/.vim/.vimrc ~/.vimrc
