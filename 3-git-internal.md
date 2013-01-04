---
layout: default
permalink: internal.html
title: ihower 的 Git 教室
---

## Git 內部原理

Git 可以說是一種用檔案內容來定位的檔案系統，SHA1 是根據內容產生的，跟檔名無關。內容一樣的檔案，即使檔案名稱不同，在*Repository*裡仍然只存一份。解耦合(decouple)了內容與當時的檔名。

Git 的 Repository 又稱作 Object Database 資料庫，共有四種 Objects 類型：
* Blob 記錄檔案內容
* Tree 記錄該目錄下有哪些檔案(檔名、內容的SHA1)和 Trees
* Commit 記錄 commit 訊息、Root tree 和 Parent commits 的 SHA1
* Tag 記錄標籤

### 觀察 Git 內部如何儲存檔案

	echo sweet > sweet.txt	git add .	find .git/objects -type f	Git 內部儲存在 .git/objects/aa/823728ea7d592acc69b36875a482cdf3fd5c8d	這是 "blob" SP "6" NUL "sweet" LF 的 SHA1	printf "blob 6\000sweet\n" | shasum	或 echo 'sweet' | git hash-object -w --stdin	git cat-file -p aa823728ea7d592acc69b36875a482cdf3fd5c8d

### 觀察 Git 內部如何儲存 Commit

	隨便抓一個 Commit 的 SHA1 開始：	git cat-file -p a08181bf3  	(觀察這個 commit，找出 tree 位置 )	git cat-file -p ea44d629  	(觀察這個 tree，找出任一個 blob SHA1)	git cat-file -p d9647d8a  	(觀察這個 blob 的內容)
	
### 參照 Reference

* Reference 會指向一個 Commit* tag 不會移動，指向的 commit 都一樣* (帶有額外資訊的 tag 內部會用 Object 儲存)* branch 指向該 branch 最新的 commit* HEAD 指向 current branch

Reference 是非常便宜的。開新 branch 和 tag 只不過是 refs 而已，直到真的有 commit 前都沒有什麼負擔。不像有些 CSV 開分支會複製一份原始碼，非常耗費資源。
### Integrity
* SHA1 是內容的 checksum * Integrity: 如果檔案內容有損毀，就會發現跟SHA1不同。如果 tree 改檔名，也會被發現。* 這在分散式系統非常重要：資料從一個開發者傳到另一個開發者時，確保資料沒有被修改
### 觀察 Git 內部如何儲存 Branch 分支
	cat .git/HEAD 拿到目前工作目錄 current branch 是指向哪一個 branch	cat .git/refs/heads/master 拿到 master branch 指向的 commit	cat .git/refs/tags/foobar 拿到 foobar tag 指向的 commit
	
了解了 Git 如何儲存 Branch 之後，就再也不會想用中央儲存式的 SVN 了：
* svn 開分支和 merge 超痛苦，能避免開 branch 就避免開 branch* svn 看 log 超痛苦，需要等待網路連線* svn commit 或 checkout 超慢，主機如果放國外常 commit 一半中斷
