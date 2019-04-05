https://gihyo.jp/magazine/wdpress/archive/2016/vol92
- ↑の本に載ってた解説が非常にわかりやすかったので参考にしてWeb開発をかじってみる


## Setting Developing Env
### Install Command Line Tools
```$ xcode-select --install```

### Install Homebrew
```$ /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"```

- ref. https://brew.sh/index_ja

> What is 'curl'
>
> サーバから、もしくはサーバへデータを転送する。コマンド。この機能の使い方の一つとしてサーバからのinstallやサーバでのAPIの実行ができる
- ref. https://qiita.com/bunty/items/758425773b2239feb9a7

### Install rbenv
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

### Install Ruby 2.3.0
```$ rbenv install 2.3.0```

### Install Rails
```$ sudo gem install rails```
gemがinstallされてなかったらbrewでinstallするかも

ここまでで開発環境の準備はひとまずOK


## 4/5 Rubyの開発環境を整える中で色々たいへんだった話
> $ bin/rails server
> /Users/noa.kusunoki/.rbenv/versions/2.3.7/lib/ruby/2.3.0/rubygems/core_ext/kernel_require.rb:55:in `require': cannot load such file -- bundler (LoadError)
	from /Users/noa.kusunoki/.rbenv/versions/2.3.7/lib/ruby/2.3.0/rubygems/core_ext/kernel_require.rb:55:in `require'
	from /Users/noa.kusunoki/git/til/web_develop/todo/bin/spring:8:in `<top (required)>'
	from bin/rails:3:in `load'
	from bin/rails:3:in `<main>'

参考：https://teratail.com/questions/63788

bundlerの再インストールで解消
> gem uninstall bundler -v 2.0.1
> gem install bundler

> $ bin/rails server


> $ bin/rails server
> Could not find rake-12.3.2 in any of the sources
> Run `bundle install` to install missing gems.

えぇ…wakaran
