# 最初に設定すべき項目

## 全ユーザ設定必須項目
gitを使い始める際に最初に必ず設定すべき項目。  
以下の設定はログインユーザ単位で反映される項目なので，全員が実施する必要がある。
<ul>
<dt>git config --global user.name "あなたの名前" </dt>
 <dd> ユーザ名称設定コマンド。  
 ユーザ名称を設定しない場合，ログイン名称などがデフォルトで使用される。  
 未設定の場合Githubへのpushが拒否されるので，実質必須設定項目。</dd>  
<dt>git config --global user.email "あなたのメールアドレス"</dt>
 <dd>ユーザ メールアドレス  
 ユーザ名称と同様に実質必須設定項目。  
 未設定の場合，ログイン名称とマシン名称からアドレスが自動生成される。</dd>  
<dt>git config --global --add merge.ff false</dt>
 <dd>fast-forwardマージを実施しない。  
 ブランチをマージする際に，fast-forward-mergeが可能であったとしても，マージコメットを発行する。  
 これにより，作業用マージが存在したというログが残る。</dd>  
<dt>git config --global --add pull.ff only</dt>
 <dd>pull時にマージを実施しない。  
 同一ブランチ内でのマージコミットを発生させないための設定。  
 この設定をしないと，不要なマージログが多発し，ログが荒れる</dd>  
 <dt>git config --global core.editor emacs</dt>
  <dd>コミット時にログを編集するエディタを設定する。  
  Windows環境で他のアプリケーションを使いたい場合，以下のコマンドとなる(らしい)  
  git config --global core.editor "'f:\tool\TeraPad\TeraPad.exe' //cu8" </dd>  
<dt>git config --global color.diff auto  
  git config --global color.status auto  
  git config --global color.branch auto  </dt>
 <dd>git diff に色付けして表示する。  
 diffの視認性を上げるために設定しておきたい項目。</dd>  
<dt>commit.template に指定されているファイルを設定</dt>
 <dd>コミット時にデフォルトで入力されている文字列を設定する。  
 要は，「コミットメッセージの雛形」ファイルを設定する。  
 プロジェクト単位で必ず記載すべき内容を決めて置くと良い。  
 後に検索を実施する際にとても重要となる項目なので，必ず実施する。  </dd>

</ul>

## Macオンリー設定

Mac ユーザーの中では有名ですが、濁点つきのディレクトリ・ファイルが分けて表示されてしまう UTF8-MAC 問題の解決方法。
忘れがちなので注意。
<ul>
<dt>git config --global core.precomposeunicode true</dt>
 <dd>グローバル設定。  
  このコマンド設定以降に，cloneした項目に有効となる。</dd>
<dt>it config --local core.precomposeunicode true</dt>
 <dd>既存のリポジトリに設定を反映するコマンド。  
 リポジトリ単位で反映される項目なので，既存のリポジトリが複数あるときは結構手間かもしれない</dd>
</ul>
<dt>git config --global core.quotepath false</dt>
 <dd>it status とかで表示される日本語ファイル名がエスケープされないようにする。</dd>

## 間違えて設定してしまった場合
<ul>
<dt>設定する値を間違えてしまった場合</dt>
 <dd>git comfig --global user.email myname@hoge.co  
  上記のように最後に「m」を付け忘れてしまった，  
  というようなケースでは正しいコマンドを実行しなおせば良い。  
  git comfig --global user.email myname@hoge.com  
  </dd>
<dt>設定する項目名を間違えてしまった場合</dt>
 <dd> 設定する項目名を間違えてしまった場合，  
 (例えば user.emilとタイプミスしてしまったなど)は以下のコマンドで設定を削除する。
 git config --unset <削除したい設定の名前></dd>
</ul>
# 設定ファイル
gitの設定ファイルには大きく分けて3種類存在する

## local
リポジトリ単位の設定を格納するフォルダ  
ファイルの所在は，  
 $TOP_DIR/.git/config


gitコマンドで値を設定する場合，「--local」オプションを設定するのが基本  
git config --local --list


## global
ユーザー単位の設定を格納するフォルダ  
ファイルの所在は  
$HOME/.gitconfig

gitコマンドで値を設定する場合，「--global」オプションを設定するのが基本  
git config --global --list

## system
マシン単位の設定を格納するフォルダ  
ファイルの所在は不明。helpには  
/etc/gitconfig
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
