# Rails Girls インストール・レシピ

<span class="muted">クッキングタイム: 5分 (作業時間) / 15-30分 (待ち時間)</span>

## 追記
## インストール時修正ポイント
```
gem 'sqlite3','~> 1.3.13'
gem 'bootsnap', '~> 1.1.0'
```

## ImageMagickのダウンロード
ダウンロードするimagemagickはこれ
https://legacy.imagemagick.org/script/download.php#windows

Ruby on Rails上にアプリケーションを作るためには、
あなたのコンピュータに必要なソフトウェアと開発環境をセットアップする必要があります。

あなたのオペレーティングシステムの説明をご覧ください。
もし、なにか問題が発生してもあわてずにコーチに声をかけてください。
コーチと一緒に問題を解決しましょう。

* [macOS 用セットアップ](#setup_for_macos)
* [Windows 用セットアップ](#setup_for_windows)


*コーチの方へ*:
インストール中に問題が発生した場合、この [Troubleshooting](https://github.com/railsgirls-jp/railsgirls-jp.github.io/wiki/Troubleshooting)  のページを参考にして下さい。

<hr />

## <a id="setup_for_macos">macOS 用セットアップ</a>

### *1.* オペレーティング・システムのバージョンを調べましょう。

Appleメニューをクリックして *About This Mac* (図 1) を選びます。

![Apple menu](/images/apple_menu.png "Apple menu")

図 1

### *2.* 開いたウィンドウに使用しているオペレーティング・システムのバージョンが表示されます。(図 2)。

バージョン番号が 10.`n` （`n` は 6 から 14の間）で始まっていたら、このドキュメントに従って進めます。
これ以外のバージョンだったら、イベントでコーチと一緒にセットアップします。

![About this Mac dialog](/images/about_this_mac.png "About this Mac dialog")

図 2

### *3.* rbenv を使って Ruby と Ruby on Rails をインストール(Mac OS X 10.9 以上の場合):

Mac OS X 10.9 以上の場合は、Homebrew と rbenv を使って環境をつくります。

#### 3-1. Command line tools をターミナルからインストール:

```
xcode-select --install
```

#### 3-2. [Homebrew](http://brew.sh/)をインストール:

```
ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```

#### 3-3. [rbenv](https://github.com/rbenv/rbenv)をインストール:

```
brew update
brew install rbenv
echo 'eval "$(rbenv init -)"' >> ~/.bash_profile
source ~/.bash_profile
```

#### 3-4. rbenvを使ってRubyをインストール:

"rbenv install -l" コマンドでrbenvでインストール可能なRubyのバージョンを確認できます。

```
rbenv install 2.6.3
```

※もしも "OpenSSL::SSL::SSLError: ... : certificate verify failed" エラーが起きた場合は、以下の手順を試してみてください。

```
brew install curl-ca-bundle
cp /usr/local/opt/curl-ca-bundle/share/ca-bundle.crt `ruby -ropenssl -e 'puts OpenSSL::X509::DEFAULT_CERT_FILE'`
```

#### 3-5. デフォルトのRuby を設定:

```
rbenv global 2.6.3
```

#### 3-6. Railsのインストール:

```
gem install rails --no-document
```

### *4.* コードを編集するのに必要なテキストエディタをインストールする。

このワークショップでは Atom エディタを推奨しています。

* [Atom エディタをダウンロードしてインストールする](https://atom.io/)

Mac OS X 10.7 およびそれ以前のバージョンでは、 Atom エディタは非対応ですが、 [Sublime Text 2](http://www.sublimetext.com/2) エディタが利用可能です。

### *5.* 動作確認

コーチの方に以下の方法で動作確認をしてもらってください。

*コーチの方へ*:

以下のコマンドでRailsが正しくインストールされているか確認してください。

```
rails new sample -B
cd sample
rails g scaffold book
rails db:migrate
rails server
```

ブラウザのURL欄に `http://localhost:3000/books` と入力して、画面が表示されれば成功です。

作ったプロジェクトは削除しておきましょう。

<hr />

## <a id="setup_for_windows">Windows 用セットアップ</a>

### *1.* Install Rails

Download [RailsInstaller](https://s3.amazonaws.com/railsinstaller/Windows/railsinstaller-3.3.0.exe) and run it. Click through the installer using the default options.

#### *1a.* Enable copy and paste in Windows Command Prompt

For Windows 10 users:

Open `Command Prompt with Ruby and Rails`.
Right-click on the command prompt’s title bar, and choose "Properties".
Navigate to the "options" tab, and check "Enable Ctrl key shortcuts".
(If you don't find it, but have an "experimental" tab,
navigate there and check "Enable new Ctrl key shortcuts" option.
In this case, you may need to check the "Enable experimental console
features" option first.)

For other Windows versions:

To paste a text in the command prompt window you'll need to use the mouse (right-click on the window --> paste).

#### *1b.* Install Rails

In the `Command Prompt with Ruby and Rails`, run the following command:

```
rails -v
```

If you see the following message:

```
the system cannot find the path specified
```

This can happen when the installer cannot correctly setup the paths required to run rails.
It's nothing serious, we can fix this in different ways but the easiest is by manually installing the rails gem with the following command:

```
gem install rails bundler --no-document
```

This will (re)install rails correctly and running:

```
rails -v
```

Should print the currently installed rails version number (your version may differ):

```
Rails 5.1.1
```

If the Rails version is less than 5.1, update it using a following command:

```
gem update rails --no-document
```

## Possible errors

### Gem::RemoteFetcher error

If you get this error when running `rails new railsgirls` or `gem update rails`:

```
Gem::RemoteFetcher::FetchError: SSL_connect returned=1 errno=0 state=SSLv3 read
server certificate B: certificate verify failed (https://rubygems.org/gems/i18n-0.6.11.gem)
```

This means you have an older version of Rubygems and will need to update it manually first verify your Rubygems version

```
gem -v
```

If it is lower than `2.6.5` you will need to manually update it:

First download the [ruby-gems-update gem](https://rubygems.org/gems/rubygems-update-2.6.11.gem). Move the file to `c:\\rubygems-update-2.6.11.gem` then run:

```
gem install --local c:\\rubygems-update-2.6.11.gem
```

```
update_rubygems --no-document
```

```
gem uninstall rubygems-update -x
```

Check your version of rubygems

```
gem -v
```

Make sure it is equal or higher than `2.6.11`. Re-run the command that was failing previously.

If you are still running into problems you can always find the latest version of rubygems online at [rubygems.org](https://rubygems.org/pages/download). If you click on **GEM** you will get the latest version.

### During bundle install

The `Gem::RemoteFetcher::FetchError: SSL_connect` can also occur during the `bundle install` stage when creating a new rails app.

The error will make mention of [bit.ly/ruby-ssl](http://bit.ly/ruby-ssl). What is relevant for Windows users at this point is [this GitHub gist](https://gist.github.com/867550). The described manual way has proven to be successful to solve the `bundle install` error.

### 'x64_mingw' is not a valid platform` Error

Sometimes you get the following error when running `rails server`:
`'x64_mingw' is not a valid platform` If you experience this error after using the RailsInstaller you have to do a small edit to the file `Gemfile`:

Look at the bottom of the file. You will probably see something like this as one of the last lines in the file:
`gem 'tzinfo-data', platforms: [:mingw, :mswin, :x64_mingw]`. If you have this line with `:x64_mingw`, then please delete the `:x64_mingw` part. In the end it should just say:
`'tzinfo-data', platforms: [:mingw, :mswin]`

After you did that, please use your Command Prompt again and type `bundle update`.

### *2.* Install a text editor to edit code files

For the workshop we recommend the text editor Atom.

* [Download Atom and install it](https://github.com/atom/atom/releases/latest)
  * Download an atom zip file for windows and decompress it.
  * Copy the folder into your Program Files.
  * Launch atom in the folder.

If you are using Windows Vista or older versions, you can use another editor [Sublime Text 2](http://www.sublimetext.com/2). Just to make sure that you're not mixing up using your command prompt or text-editor: change the theme of your Sublime text-editor, choosing one of the following: "iPlastic", "Slush &amp; Poppies", or "Zenburnesque".

### *3.* Install Node.js

* Go to [https://nodejs.org/](https://nodejs.org/) and install Node.js LTS package
* Reopen your Rails Command Shell

Check your version of node

```
node --version
```

Make sure it is displaying version number.

### *4.* Check the environment

Check that everything is working by running the application generator command.

```
rails new myapp -B
```

```
cd myapp
```

```
rails server
```

Go to `http://localhost:3000` in your browser, and you should see the 'Yay! You're on Rails!' page.

Now you should have a working Ruby on Rails programming setup. Congrats!

**Coach:** We recommend to verify by using the scaffold command and inputting data with the generated page with coaches to ensure everything is working. Also: remove the test app `myapp` to make super sure no-one is working in the wrong folder, following the steps of the workshop.

