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

### 4/16 続き
久々に叩いてみた
> $ bin/rails server
> Could not find rake-12.3.2 in any of the sources
> Run `bundle install` to install missing gems.
> $ bundle install

おや、メッセージが変わった
```
(前略)
HEADS UP! i18n 1.1 changed fallbacks to exclude default locale.
But that may break your application.

Please check your Rails app for 'config.i18n.fallbacks = true'.
If you're using I18n (>= 1.1.0) and Rails (< 5.2.2), this should be
'config.i18n.fallbacks = [I18n.default_locale]'.
If not, fallbacks will be broken in your app by I18n 1.1.x.

For more info see:
https://github.com/svenfuchs/i18n/releases/tag/v1.1.0

Post-install message from chromedriver-helper:

  +--------------------------------------------------------------------+
  |                                                                    |
  |  NOTICE: chromedriver-helper is deprecated after 2019-03-31.       |
  |                                                                    |
  |  Please update to use the 'webdrivers' gem instead.                |
  |  See https://github.com/flavorjones/chromedriver-helper/issues/83  |
  |                                                                    |
  +--------------------------------------------------------------------+

Post-install message from sass:

Ruby Sass has reached end-of-life and should no longer be used.

* If you use Sass as a command-line tool, we recommend using Dart Sass, the new
  primary implementation: https://sass-lang.com/install

* If you use Sass as a plug-in for a Ruby web framework, we recommend using the
  sassc gem: https://github.com/sass/sassc-ruby#readme

* For more details, please refer to the Sass blog:
  https://sass-lang.com/blog/posts/7828841
```
なんのこっちゃ。
とりあえず、指示に従ってconfigを見てみた
> $grep -r 'config.i18n' ./
> .//config/environments/production.rb:  config.i18n.fallbacks = true

ヨシ。
そして、、、
> bin/rails server
=> Booting Puma
=> Rails 5.2.3 application starting in development
=> Run `rails server -h` for more startup options
Puma starting in single mode...
* Version 3.12.1 (ruby 2.3.7-p456), codename: Llamas in Pajamas
* Min threads: 5, max threads: 5
* Environment: development
* Listening on tcp://localhost:3000
Use Ctrl-C to stop

動いたー！
この状態でブラウザで http://localhost:3000 にアクセスするとデフォルトのRails画面が表示されるらしい。問題なし。

### Create Table
> 参考：https://techacademy.jp/magazine/7207
上だととりあえずDBを作る、削除するなどのコマンド操作を教えてるけど、本では最初にマイグレーションファイルを作ることから始める。
> $ bin/rails g migration CreateTasks content:text status:integer{4}
> Running via Spring preloader in process 42281
>      invoke  active_record
>      create    db/migrate/20190416121834_create_tasks.rb

問題なさそう。生成されたファイルの中身を見ても気になるところはなし。ついで起動もつつがなく完
>  bin/rake db:migrate
> Running via Spring preloader in process 42417
> == 20190416121834 CreateTasks: migrating ======================================
> -- create_table(:tasks)
>    -> 0.0014s
> == 20190416121834 CreateTasks: migrated (0.0015s) =============================

