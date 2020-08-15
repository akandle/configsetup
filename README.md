# ConfigSetup
> This is a repository of configuration, setup, and installation files as well as directions.  The main purpose of this repo is to capture those tidbits of knowledge where being an expert is not the primary goal, but rather usability and an emphasis on re-usability.  One main objective is to also enable scriptability so proper and methodical structure will be of utmost importance.

## Android
### TODO
 - Make this a script
 - Compartmentalize each action and then build into a single script
 - Testing will be hard to accomplish unless each dependant project does testing somehow
 - Round up all dotfiles.  There is an untracked my_configs.vim on the tablet.  Need to somehow control versioning and centralize the source so all devices using a particular platform, such as termux, have identical configs and can make and push changes as well
### base installation
```
pkg update
pkg upgrade
pkg install python cmake nodejs ruby golang
// note here: golang doesnt download, just install what is needed
pkg install vim tmux git
```

### vim-awesome
```
git clone depth=1 https://github.com/amix/vimrc.git ~/.vim_runtime
sh ~/.vim_runtime/install_awesome_vimrc.sh
```

### folder structure
```
cd
mkdir -v gh projects
```

### dot files
> These are specific to termux on android and should be edited anyway
```
cd ~/gh
git clone https://github.com/konradit/dotfiles.git
cp dotfiles/bashrc ~/.bashrc
// Note: Should be symbolicly linked so it stays "current"
```

### additional tools and misc
```
pkg install coreutils termux-api termux-exec termix-tools grep tree ncurses-utils openssh gnupg
```

### postgresql install / setup
```
pkg install postgresql
mkdir -p $PREFIX/var/lib/postgresql
initdb $PREFIX/var/lib/postgresql

// Start DB
pg_ctl -D $PREFIX/var/lib/postgresql start

// Stop DB
pg_ctl -D $PREFIX/var/lib/postgresql stop

// Create DB User *replace userName
createuser --superuser --pwprompt userName

// Create a Database *replace MyDB
createdb myDB

// Open DB *replace myDB
psql myDB
```

### Oh My TMUX
- I wonder how useful this really is. DO NOT put the git repo in the home directory
```
cd ~/gh
git clone https://github.com/gpakosz/.tmux.git
cd ~
ln -s -f ./gh/.tmux/.tmux.conf
cp ./gh/.tmux/.tmux.conf.local .
```

### Oh My ZSH
```
cd ~/gh
git clone https://github.com/adi1090x/termux-omz.git
cd termux-omz
chmod +x setup
./setup
```

## Git Setup

### HTTPS Credential caching
> Activate the credential cache
```
git config --global credential.helper cache
```
> Change the default password cache timeout, setting is in seconds (1 hour in example)
```
git config --global credential.helper 'cache --timeout=3600'
```
## Desktop - Ubuntu
### Oh My ZSH
```sh -c "$(curl -fsSL https://raw.github.com/ohmyzsh/ohmyzsh/master/tools/install.sh)" ```
