---
layout: default
permalink: remote.html
title: Git 團隊協同開發指令
---

# Git 團隊協同開發指令

上一章介紹了在本地端用`git init`初始了一個*Repository*。不過，比較常的情況是你是從拷貝一個已經存在的 Repository 開始開發。Git 有以下四種方法來存取遠端的*Git*伺服器：

* SSH 安全性最佳
	* git clone git@github.com:ihower/sandbox.git
* HTTP/HTTPS 速度最差，但能突破防火牆限制
	* git clone https://ihower@github.com/ihower/sandbox.git
* File 本機目錄 (有人用 Dropbox 分享 git init --bare --shared 目錄!! Crazy!!)
	* git clone file://path/to/repo.git

## 以 GitHub Repository 為例

[GitHub](http://github.com) 是基於 Git 這套分散式版本控制系統的 Repository hosting 應用，只要是開放原始碼軟體，都可以免費的使用這個服務。這裡就使用*Github*來進行練習：

## 在 Github 上建立一個專案

	產生 SSH Key
	ssh-keygen -t rsa -C "your_email@youremail.com"
	至 Github 註冊，設定你的 SSH Public Key，並開一個專案
	git remote add origin git@github.com:your_account/sandbox.git
	git push -u origin master
	之後只需要 git push
	出現 ![rejected] 表示需要先做 git pull

編輯專案的 Settings，加入別人成為你專案的 Collaborators。這樣別人就可以用 SSH 協定來 clone 你的專案。
### 在 Github 上	Clone 下來

以筆者的專案 [Sandbox](https://github.com/ihower/sandbox) 為例，如果你有寫入權限的話(被加入成Collaborators)，就可以用 SSH 協定 Clone 下來：

	git clone git@github.com:ihower/sandbox.git

如果有防火牆問題，改用 HTTPS 協定：

	git clone https://github.com/ihower/sandbox.git

## Pull - 從遠端更新

	git pull 或 git pull origin master

實際作用是先 git fetch 遠端的 branch，然後與本地端的 branch 做 merge，產生一個 merge commit 節點

> 所謂的"遠端"預設叫做*origin*，當你有多個不同遠端伺服器時，就會取不同名子了。

## Push - 將 Commit 送出去

	git push 或 git push origin master

實際的作用是將本地端的 master branch 與遠端的 master branch 作 fast-forward 合併。如果出現 [rejected] 錯誤的話，表示你必須先作 pull。
預設不會 push tags 資訊：
	git push --tags

## 列出和取出遠端 branch

	git branch -r
	git checkout -t origin/foobar
	git branch -r --merged (列出已經被合併的)

## 刪除遠端 Branch

	git push origin :foobar
	git pull 和 git fetch 不會清除已經被刪掉的 branch
	請用 git fetch -p

## git push --tags

	預設不會 push tags 資訊
	git push --tags

## git pull --rebase

使用`git pull --rebase`可以避免無謂的 merge 節點，讓線圖變乾淨，是個非常有用的小技巧，特別是很多人在同一個 branch 同時開發的情況。

請參考[使用 git rebase 避免無謂的 merge](http://ihower.tw/blog/archives/3843)。
