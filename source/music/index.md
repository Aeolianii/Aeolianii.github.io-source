---
title: music
date: 2025-07-03 12:40:41
type: "music"
---

<!-- 引入 APlayer CSS 和 JS -->
<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/aplayer@1.10.4/dist/APlayer.min.css">
<script src="https://cdn.jsdelivr.net/npm/aplayer@1.10.4/dist/APlayer.min.js"></script>

<!-- 播放器容器 -->
<div id="aplayer"></div>

<script>
// 等待 DOM 加载完成后初始化播放器
document.addEventListener('DOMContentLoaded', function() {
  const ap = new APlayer({
    container: document.getElementById('aplayer'),
    fixed: true,
    autoplay: false,
    theme: '#3EAF7C',
    audio: [
      {
        name: 'Anomaly',
        artist: 'Lights & Motion',
        url: '/music/Anomaly.mp3',
        cover: '/music/Anomaly.jpg'
      }
    ]
  });
});
</script>
