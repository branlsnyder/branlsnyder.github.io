---
layout: post
title: ""
subtitle: "Brandon Woo Snyder & Xuanqi Liu"
category: []
# tags: [live electronics, concatenative synthesis, diffusion]
image: 
slug: xuanqi-brandon
---



<h2>...a duo with <a href="/about" class="keywordrand">Brandon Woo Snyder</a> & <a href="https://www.xuanqiliu.com/" class="keywordrand">Xuanqi Liu</a> </h2>

<div class="duo-images">
  <a href="https://www.xuanqiliu.com/" class="duo-image-link" id="xuanqi-link">
    <img
      id="home-headshot"
      class="home-image"
      src="/assets/img/xuanqi-headshot.jpg"
      alt="Xuanqi Liu"
      decoding="async"
    />
  </a>

  <a href="/about" class="duo-image-link" id="brandon-link">
    <img
      id="duo-smore-thumb"
      class="home-image"
      src="/assets/img/smore-thumb.jpg"
      alt="S'more"
      decoding="async"
    />
  </a>
</div>

<script>
  document.addEventListener("DOMContentLoaded", () => {
    const { createDraggable } = anime;
    const images = [
      ["home-headshot", "/assets/img/xuanqi-headshot.jpg"],
      ["duo-smore-thumb", "/assets/img/smore-thumb.jpg"],
    ];

    images.forEach(([id, src]) => {
      const img = document.getElementById(id);
      if (!img) return;
      img.src = src;

      const imgRect = img.getBoundingClientRect();
      const imgX = imgRect.left + window.scrollX;
      const imgY = imgRect.top + window.scrollY;
      createDraggable(img, {
        container: () => {
          const docH = document.documentElement.scrollHeight;
          const vw = window.innerWidth;
          const sx = window.scrollX;
          return [
            -imgY,
            vw - imgX - imgRect.width + sx,
            docH - imgY - imgRect.height,
            -imgX + sx,
          ];
        },
        containerFriction: 1,
        releaseContainerFriction: 0.8,
      });
    });

    // Clicking an image opens its link; dragging it should not.
    document.querySelectorAll(".duo-image-link").forEach((link) => {
      let pressing = false;
      let startX = 0;
      let startY = 0;
      let moved = 0;

      link.addEventListener("pointerdown", (e) => {
        pressing = true;
        startX = e.clientX;
        startY = e.clientY;
        moved = 0;
      });
      window.addEventListener("pointermove", (e) => {
        if (!pressing) return;
        moved = Math.max(moved, Math.hypot(e.clientX - startX, e.clientY - startY));
      });
      window.addEventListener("pointerup", () => {
        pressing = false;
      });
      link.addEventListener("click", (e) => {
        if (moved > 5) e.preventDefault();
      });
    });
  });
</script>