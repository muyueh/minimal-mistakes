---
layout: default
title: "隨機 Skin 預覽"
permalink: /skin-preview/
---

<div class="page__inner-wrap">
  <header>
    <h1 class="page__title">隨機 Skin 預覽</h1>
    <p class="page__lead">按一下隨機按鈕，即可快速套用 Minimal Mistakes 的各種配色。</p>
  </header>

  <div class="notice--info">
    <p>這個頁面會為你載入主題的另一份樣式表，並覆蓋預設的 <code>minimal_mistakes_skin</code> 設定，方便即時預覽。</p>
  </div>

  <div class="skin-preview__controls">
    <button class="btn btn--primary" id="random-skin">🎲 隨機選擇 Skin</button>
    <span class="skin-preview__label">目前顯示：<strong id="current-skin" aria-live="polite">載入中…</strong></span>
  </div>

  <div class="skin-preview__sample">
    <h2>標題樣式</h2>
    <p>這裡會使用隨機配色呈現。你也可以瀏覽頁面其他區塊，檢查背景、文字與按鈕顏色是否符合需求。</p>
    <div class="btn-group">
      <a class="btn" href="#">一般按鈕</a>
      <a class="btn btn--primary" href="#">主要按鈕</a>
      <a class="btn btn--info" href="#">資訊按鈕</a>
    </div>
  </div>
</div>

<style>
  .skin-preview__controls {
    display: flex;
    gap: 1rem;
    align-items: center;
    margin: 1rem 0 1.5rem;
  }

  .skin-preview__label {
    font-size: 1rem;
  }

  .skin-preview__sample {
    padding: 1.25rem;
    border-radius: .5rem;
    border: 1px solid var(--border-color, #e5e5e5);
    background-color: var(--background-color, #fff);
  }
</style>

<script>
  (function () {
    const skins = [
      "default",
      "air",
      "aqua",
      "contrast",
      "dark",
      "dirt",
      "mint",
      "neon",
      "plum",
      "sunrise"
    ];

    const randomButton = document.getElementById("random-skin");
    const skinName = document.getElementById("current-skin");
    const skinBase = "{{ '/assets/css/skins/' | relative_url }}";

    const skinLink = document.createElement("link");
    skinLink.rel = "stylesheet";
    skinLink.id = "skin-style";
    document.head.appendChild(skinLink);

    function applySkin(name) {
      skinLink.href = `${skinBase}${name}.css`;
      skinName.textContent = name;
    }

    function randomSkin() {
      const index = Math.floor(Math.random() * skins.length);
      applySkin(skins[index]);
    }

    randomButton.addEventListener("click", randomSkin);
    randomSkin();
  })();
</script>
