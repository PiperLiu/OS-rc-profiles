# rc files
## Very Basic Profile
### Linux
When getting a Linux server, `~/.vimrc` it: [.vimrc](./.vimrc), no need for any plugins.

Then `zsh`:
```
# install zsh (Ubuntu)
apt-get install zsh

# install oh-my-zsh
sh -c "$(curl -fsSL https://raw.github.com/robbyrussell/oh-my-zsh/master/tools/install.sh)"

# cat shells
cat /etc/shells

# default shell is zsh
chsh -s /bin/zsh

# create profile
cp ~/.oh-my-zsh/templates/zshrc.zsh-template ~/.zshrc

# install one plugin : zsh-syntax-highlighting
cd ~/.oh-my-zsh/plugins
git clone https://github.com/zsh-users/zsh-syntax-highlighting.git
```
Then, `~/.zshrc`: [.zshrc](./zshrc).

### 
