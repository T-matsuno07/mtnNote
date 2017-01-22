# stash
ブランチを切り替え(checkout)したり，pullした時に，未commitの作業内容を一時的に保管しておくコマンド。

### git stash save
 作業内容を保存する。  
 stashの後の文字列を省略した場合，saveコマンドが実施される。
### git stash list
 saveコマンドで保存した作業内容の一覧を表示する
### git stash pop <復元対象>
 saveコマンド保存した内容を復元するコマンド。  
 復元と同時にstash内容を削除する。  
 saveコマンドによって保存した情報を復元する際に最もよく使えるコマンド。

### git stash drop <削除対象>
 saveしたstashを削除する。
### git stash apply <復元対象>
 saveコマンドで保存した内容を復元するコマンド。  
 applyとは異なり，復元した後もstash情報は残る。
