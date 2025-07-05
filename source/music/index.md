---
title: music
date: 2025-07-03 12:40:41
type: "music"
---

<!-- 引入 APlayer CSS 和 JS -->
<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/aplayer@1.10.1/dist/APlayer.min.css">
<script src="https://cdn.jsdelivr.net/npm/aplayer@1.10.1/dist/APlayer.min.js"></script>

<!-- 播放器容器 -->
<div id="aplayer"></div>

<script>
// 初始化播放器（仅一首纯音乐，无歌词）
const ap = new APlayer({
  container: document.getElementById('aplayer'),
  fixed: true,  // 固定在底部
  autoplay: false,  // 不自动播放
  theme: '#3EAF7C',  // 主题色
  audio: [
    {
      name: 'Anomaly',  // 显示的歌曲名称
      artist: 'Lights & Motion',    // 显示的艺术家
      url: '/music/Anomaly.mp3',  // 本地 MP3 文件路径
      cover: '/music/Anomaly.jpg'  // 随机封面图（可替换为自己的图）
    }
  ]
});
</script>
