---
layout: default
permalink: internal.html
title: ihower 的 Git 教室
---

## Git 內部原理

Git 可以說是一種用檔案內容來定位的檔案系統，SHA1 是根據內容產生的，跟檔名無關。內容一樣的檔案，即使檔案名稱不同，在*Repository*裡仍然只存一份。解耦合(decouple)了內容與當時的檔名。

Git 的 Repository 又稱作 Object Database 資料庫，共有四種 Objects 類型：

* Tree 記錄該目錄下有哪些檔案(檔名、內容的SHA1)和 Trees
* Commit 記錄 commit 訊息、Root tree 和 Parent commits 的 SHA1
* Tag 記錄標籤

### 觀察 Git 內部如何儲存檔案

	echo sweet > sweet.txt

### 觀察 Git 內部如何儲存 Commit

	隨便抓一個 Commit 的 SHA1 開始：

### 參照 Reference

* Reference 會指向一個 Commit

Reference 是非常便宜的。開新 branch 和 tag 只不過是 refs 而已，直到真的有 commit 前都沒有什麼負擔。不像有些 CSV 開分支會複製一份原始碼，非常耗費資源。





了解了 Git 如何儲存 Branch 之後，就再也不會想用中央儲存式的 SVN 了：

