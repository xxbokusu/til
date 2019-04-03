https://gihyo.jp/magazine/wdpress/archive/2016/vol92
↑の本に載ってた解説が非常にわかりやすかったので参考にしてWeb開発をかじってみる


## Setting Developing Env
- Install Command Line Tools
```$ xcode-select --install```

- Install Homebrew
```$ /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"```
ref. https://brew.sh/index_ja

> What is 'curl'

## Install rbenv
```
$ brew install rbenv
$ vim ~/.bash_profile 
# eval "$(rbenv init -)"
# echo 'export PATH="$HOME/.rbenv/bin:$PATH"' >> ~/.bash_profile を追記
$ source ~/.bash_profile
```
ref. 
- https://qiita.com/Alex_mht_code/items/d2db2eba17830e36a5f1
- https://github.com/rbenv/rbenv のReadme

## Install Ruby 2.3.0
```$ rbenv install 2.3.0```

## Install Rails
```$ sudo gem install rails```
gemがinstallされてなかったらbrewでinstallするかも

ここまでで開発環境の準備はひとまずOK

