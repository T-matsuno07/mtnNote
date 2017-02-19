# Git notes ログ機能まとめ

Gitのコミットログは，Gitで管理しているプロジェクトにおいて，ノウハウを残すために非常に重要な情報である。
しかし，Gitのログには，重大な弱点が存在する。


それは，`コミットログを後から書き直すことができない`という制約である。


pushのよりコミット情報をリモートリポジトリに送信する前であれば，amendコマンドにより，ローカルリポジトリのコミットログを書き直すことが出来る。  
しかし，push済みのコミットについては，コミットログを書き直す手段が存在しない。

そのため，Gitには，コミットログとは別に，好きな時に自由に書き換えることが出来る注釈をコミットに付与することができる`notes`という機能が備わっている。  


本ページでは，その`notes`機能についてまとめる。


## notes情報をpush

notes の情報は通常の push とは別に push する必要があります

```bash
$ git push origin refs/notes/commits
```

~/.gitconfig に追加
```bash
[alias]
   pushnotes = "!sh -c 'git push $1 refs/notes/*' -"
```

alias で呼び出し

```bash
$ git pushnotes origin
```

## notes情報をfetch

fetch も push と同じく別途 fetch する必要があります

```bash
$ git fetch origin refs/notes/commits:refs/notes/commits
```
~/.gitconfig に追加
```bash
[alias]
   fetchnotes = "!sh -c 'git fetch $1 refs/notes/*:refs/notes/*' -"
```   
alias で呼び出し
```bash
$ git fetchnotes origin
```
