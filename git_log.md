# Git logコマンドまとめ

## コマンド例
一行目: [日付]　短縮ハッシュ値 コミット者名  
二行目: ログ 及び ノート
```bash
git log --date=short --pretty=format:"%Cred[%cd] %Cblue%h %Cgreen%cn %n%Creset%B%N"
```

- --graph  
フラグを指定すると、コミットメッセージの左側にテキストベースでコミット履歴をグラフ化したもの描画します。
- --decorate  
フラグを指定すると、表示されているコミットのブランチ名やタグ名を追加して表示します。
- --oneline  
 フラグを指定するとコミット情報を圧縮して1行に表示するためコミット履歴の概観に便利です。

```bash
git log --graph --decorate ﻿--oneline
```

## format オプション 記述用マクロ
git logで出力する情報やフォーマットをカスタマイズしたい場合，
prettyオプションを使うと良い。  

```
git log --pretty=[オプション]
```
しかし，デフォルトで用意されているオプションは，
いずれも出力される情報やフォーマットが微妙なので，自分好みにカスタマイズ出来る
pretty=formatの組み合わせが抜群に使い勝手が良い。  
```
git log --pretty=format:"[オプション]"
```

以下，formatで使えるオプション一覧

|オプション|	内容|
|:---|:---|
|%n|改行 |
|%H|	コミットのハッシュ|
|%h|	コミットのハッシュ (短縮版)|
|%T|	ツリーのハッシュ|
|%t|	ツリーのハッシュ (短縮版)|
|%P|	親のハッシュ|
|%p|	親のハッシュ (短縮版)|
|%an|	Author の名前|
|%ae|	Author のメールアドレス|
|%ad|	Author の日付 (-date= オプションに従った形式。詳細は後述)|
|%ar|	Author の相対日付|
|%cn|	Committer の名前|
|%ce|	Committer のメールアドレス|
|%cd|	Committer の日付|
|%cr|	Committer の相対日付|
|%s	| ログ(改行なし)|
|%Cred| 色オプション 赤|
|%Cblue| 色オプション 青|
|%Cgreen| 色オプション 緑|
|%Creset| 色オプション デフォルトに戻す|


## date オプション 記載方法
```bash
--date=[オプション]
```
幾つか種類があるが，使い勝手が良いのは，「short」と「relative」の2つ。他は，あまり使う機会がないかもしれない。

|オプション|	内容|
|:-|:-|
|relative|	相対時間 (3 days ago)|
|local|	ローカルタイムゾーン|
|iso|	ISO 8601 フォーマット|
|rfc|	RFC 2822 フォーマット|
|short|	YYYY-MM-DD|
|raw|	%s %z|
|default|	標準|

## 修正したファイル名を表示
各コミットで変更を加えたファイル名を表示するオプション。  
出力する情報量とフォーマットのバランスが良いのは，「--name-status」

|オプション|	内容|
|:-|:----|
|--stat| ファイル名<p>各ファイルの追加行数/削除行数(グラフ形式)<p>コミット全体の追加/削除行数 |
|--numstat | ファイル名<p>各ファイルの追加行数/削除行数 |
|--name-status| ファイル名<p>各ファイルの変更種別(変更/新規追加/削除)|
|--name-only| ファイル名のみ|

## 特定のログのみを表示する

### grep
コミットメッセージが <pattern>  (プレーンテキストまたは正規表現) と一致するコミットを検索します。
```bash
git log --grep="<pattern>"
```
