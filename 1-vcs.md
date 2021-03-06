---
layout: default
permalink: vcs.html
title: 版本控制系統簡介
---

# 版本控制系統

## 原因

在軟體開發的過程中，程式碼每天不斷地產出，過程中會發生以下情況：

1. 檔案被別人或自己覆蓋，甚至遺失
2. 想復原前幾天寫的版本
3. 想知道跟昨天寫的差在哪裡
4. 是誰改了這段程式碼，為什麼
5. 軟體發行，需要分成維護版跟開發版

因此，我們希望有一種機制，能有幫助我們：

1. 可以隨時復原修改，回到之前的版本
2. 多人協作時，不會把別人的東西蓋掉
3. 保留修改歷史記錄，以供查詢
4. 軟體發行時，可以方便管理不同版本

## 定義

一個版本控制系統 Version Control System (VCS)，通常有以下功能

1. 建立 Repository (儲存庫)，用來保存程式碼。
2. 方便散佈程式給團隊，有效率協同開發 z
3. 記錄誰改變什麼、在什麼時候、因為什麼原因 z
4. Branch(分支)，可因不同情境分開開發
5. Tag(標籤) 重要里程碑，以便參照

那麼，什麼東西要存進*Repository*呢? 簡單來說，就是所有跑起來這個專案需要的東西，包括所有原始碼、範例設計檔、文件等等。而像是暫存檔、log 檔案、build files 等編譯後的產物則不需要存進 *Repository*。

## 演進歷史

版本控制系統從古至今，有幾種不同的模式：

### Local VCS

本地端使用 copy paste 進行資料夾管理，例如 rcs。當然，缺點是無法協同開發。

### Centralized VCS (Lock型，悲觀鎖定)

有一台中央團隊共用的*Repository*，當有人要編輯某個檔案時，進行鎖定，以避免其他人也同時編輯造成衝突。

雖然可以避免衝突，但是很不方便。其他人得排隊才能編輯檔案，萬一先取出的人寫很久或忘記 unlock...

### Centralized VCS(Merge型，樂觀鎖定)

也是有一台中央團隊共用的*Repository*，但是不用*Lock*來避免衝突，而是事後發現如果有別人也修改同一個檔案(稱作衝突)，再進行手動編修解決。
有非常多的VCS屬於這一型，包括CVS, Subversion, Perforce等等。

Centralized VCS 的共同缺點是做什麼事都要跟伺服器連線，會比較慢。另外也有單點故障的風險(Single point of failure)，只要伺服器壞掉，大家就不用作事了。

### Distributed VCS

分散式版本控制系統讓本地端也擁有完整的*Repository*，就沒有上述集中式的問題，即使沒網路，照常可以 commit 和看 history log，也不用擔心server備份。
例如 Git, Mercurial(Hg), Bazaar 等就是屬於分散式版本控制系統。

若要說有什麼缺點，就是能力越大，功能就越複雜，一開始學習上會比較辛苦一點。

## 參考資料

* [旅行必備、居家良伴、送禮自用兩相宜的「版本控制系統」](http://jedi.org/blog/archives/004784.html)
* [那些台灣軟體產業所缺少的 – 版本控制系統](http://blog.ez2learn.com/2011/10/20/taiwan-software-lacking-of-vcs/)

