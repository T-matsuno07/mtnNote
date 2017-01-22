# stash
ブランチを切り替え(checkout)したり，pullした時に，未commitの作業内容を一時的に保管しておくコマンド。

<ur>
<dt>git stash save </dt>
 <dd>作業内容を保存する</dd>
<dt>git stash list </dt>
 <dd>saveコマンドで保存した作業内容の一覧を表示する</dd>
<dt>git stash pop <復元対象></dt>
 <dd>saveコマンド保存した内容を復元するコマンド。  
 復元と同時にstash内容を削除する</dd>
<dt>git stash drop <削除対象></dt>
 <dd>saveしたstashを削除する。</dd>
<dt>git stash apply <復元対象></dt>
 <dd>saveコマンドで保存した内容を復元するコマンド。  
 applyとは異なり，復元した後もstash情報は残る</dd>

</ur>
