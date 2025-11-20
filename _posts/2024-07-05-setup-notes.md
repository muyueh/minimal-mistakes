---
layout: single
title: "建置紀錄：GitHub Pages × Minimal Mistakes"
date: 2024-07-05 10:30:00 +0800
categories: [技術]
tags: [Github Pages, Jekyll, Minimal Mistakes]
excerpt: "記下建立部落格的步驟，避免下次重來又忘了。"
---

這次的設定流程大致如下：

1. 在 GitHub 建立 `<username>.github.io` 儲存庫，啟用 Pages。
2. 在 `_config.yml` 指定 `remote_theme: "mmistakes/minimal-mistakes"`，選擇喜歡的 skin（我選擇 `mint`）。
3. 加入 `_posts/YYYY-MM-DD-title.md`，用 `layout: single` 即可帶出標題、日期、標籤。
4. 如果要留言系統，可以考慮 giscus；之後再來補。

這篇文章也算是對自己的提醒：文件都寫在 repo 裡，換機器或重裝也不用怕忘記。
