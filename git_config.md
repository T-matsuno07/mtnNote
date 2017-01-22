# 最初に設定すべき項目

## 全ユーザ設定必須項目
gitを使い始める際に最初に必ず設定すべき項目。  
以下の設定はログインユーザ単位で反映される項目なので，全員が実施する必要がある。

### git config --global user.name "あなたの名前"
 ユーザ名称設定コマンド。   
 ユーザ名称を設定しない場合，ログイン名称などがデフォルトで使用される。  
 未設定の場合Githubへのpushが拒否されるので，実質必須設定項目。

### git config --global user.name "あなたの名前"
  ユーザ名称設定コマンド。  
  ユーザ名称を設定しない場合，ログイン名称などがデフォルトで使用される。  
  未設定の場合Githubへのpushが拒否されるので，実質必須設定項目。

### git config --global user.email "あなたのメールアドレス"
 ユーザ メールアドレス  
 ユーザ名称と同様に実質必須設定項目。  
 未設定の場合，ログイン名称とマシン名称からアドレスが自動生成される。
### git config --global --add merge.ff false
 fast-forwardマージを実施しない。  
 ブランチをマージする際に，fast-forward-mergeが可能であったとしても，マージコメットを発行する。  
 これにより，作業用マージが存在したというログが残る。
### git config --global --add pull.ff only
 pull時にマージを実施しない。  
 同一ブランチ内でのマージコミットを発生させないための設定。  
 この設定をしないと，不要なマージログが多発し，ログが荒れる

### git config --global core.editor emacs
  コミット時にログを編集するエディタを設定する。  
  Windows環境で他のアプリケーションを使いたい場合，以下のコマンドとなる(らしい)  
  git config --global core.editor "'D:\ProgramFiles\sakura\sakura.exe'"


### git config --global color.* auto
  git config --global color.diff auto  
  git config --global color.status auto  
  git config --global color.branch auto

  git diff に色付けして表示する。  
 diffの視認性を上げるために設定しておきたい項目。  

### git config --global push.default simple
pushコマンドを引数未指定で実行した際の挙動を設定します。
gitのバージョンが古い場合，この設定を行わないとpushの度に警告文が表示されるので最初に設定しておくこと。

### commit.template に指定されているファイルを設定
 コミット時にデフォルトで入力されている文字列を設定する。  
 要は，「コミットメッセージの雛形」ファイルを設定する。  
 プロジェクト単位で必ず記載すべき内容を決めて置くと良い。  
 後に検索を実施する際にとても重要となる項目なので，必ず実施する。

## Macオンリー設定

Mac ユーザーの中では有名ですが、濁点つきのディレクトリ・ファイルが分けて表示されてしまう UTF8-MAC 問題の解決方法。
忘れがちなので注意。
### git config --global core.precomposeunicode true
  グローバル設定。  
  このコマンド設定以降に，cloneした項目に有効となる。
### git config --local core.precomposeunicode true
 既存のリポジトリに設定を反映するコマンド。  
 リポジトリ単位で反映される項目なので，既存のリポジトリが複数あるときは結構手間かもしれない。
### git config --global core.quotepath false</dt>
 git status とかで表示される日本語ファイル名がエスケープされないようにする。

## 間違えて設定してしまった場合

### 設定する値を間違えてしまった場合

- git comfig --global user.email myname[at]]hoge.co  
  上記のように最後に「m」を付け忘れてしまった，  
  というようなケースでは正しいコマンドを実行しなおせば良い。  
  git comfig --global user.email myname[at]hoge.com  

### 設定する項目名を間違えてしまった場合
- git config --unset <削除したい設定の名前>  
 設定する項目名を間違えてしまった場合，  
 (例えば user.emilとタイプミスしてしまったなど)は以下のコマンドで設定を削除する。

# コマンドを短縮形を有効にする
gitコマンドを実効する際に，毎回gitコマンドを全て入力していると作業効率が下がってしまうので，git用のalias登録をしておくと良い。
ホームディレクトリ直下に存在する「.gitconfig」に以下の内容を入力する。  
「vi ~/.gitconfig」  
```bash
[alias]
    ad = add
    br = branch
    ci = commit
    co = checkout
    ft = fetch
    pl = pull
    ps = push
    sh = show
    st = status
```

# 設定ファイルの所在
gitの設定ファイルには大きく分けて3種類存在する

## local
リポジトリ単位の設定を格納するフォルダ  
ファイルの所在は，  
`` $TOP_DIR/.git/config``


gitコマンドで値を設定する場合，「--local」オプションを設定するのが基本  
``git config --local --list``


## global
ユーザー単位の設定を格納するフォルダ  
ファイルの所在は  
``$HOME/.gitconfig``

gitコマンドで値を設定する場合，「--global」オプションを設定するのが基本  
``git config --global --list``

## system
マシン単位の設定を格納するフォルダ  
ファイルの所在は不明。helpには  
``/etc/gitconfig``
と記載があるが。。。。

gitコマンドで値を設定する場合，「--system」オプションを設定するのが基本  
git config --system --list



# mergeの設定
## ブランチをマージする際にfast-forwardマージを許可しない
git config --global --add merge.ff false

異なる2つのブランチをマージする際は，
必ず「元々は別々のブランチだった」という情報を残す。

## 同一ブランチ内ではマージを行わない
git config --global --add pull.ff only

svnに近い挙動にする。  
同一ブランチに他の人が先にpushしている時，rebaseするようにする。
