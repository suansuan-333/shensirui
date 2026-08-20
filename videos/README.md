# 视频文件说明

本目录存放作品集弹窗内播放的视频文件。HTML 中已通过 `videos/视频编号.mp4` 引用。

## 当前文件

| 文件名 | 对应项目 | 状态 |
|---|---|---|
| `video4.mp4` | AIGC 视频《灰烬之花》（ai1） | 已上传 |
| `video5.mp4` | 短纪录片《沙磁乱针绣》（video5） | 已上传 |

待补充：`video1.mp4`、`video2.mp4`、`video3.mp4`、`video6.mp4`、`video7.mp4`、`video8.mp4`。

## 命名规则

与 `deploy_portfolio/index.html` 中 `projectData` 的 `video.sources` 保持一致：

```js
video: {
  poster: 'images/works/video1_1.png',
  sources: [{ src: 'videos/video1.mp4', type: 'video/mp4' }]
}
```

如需新增格式（如 WebM），在 `sources` 数组追加即可，播放器会自动按顺序回退。

## 格式建议

- **封装**：MP4（H.264/AAC），兼容性最好；可额外准备 WebM 做备用。
- **分辨率**：建议 1920×1080 或 1280×720。
- **码率**：
  - 1-3 分钟短片：3-6 Mbps
  - 5-35 分钟长片：1.5-3 Mbps
- **文件大小**：单文件控制在 100MB 以内，避免首次加载过慢；长片可分段或压缩。
- **编码工具**：剪映导出选 H.264；FFmpeg 示例：
  ```bash
  ffmpeg -i input.mov -c:v libx264 -preset slow -crf 23 -c:a aac -b:a 128k -movflags +faststart output.mp4
  ```

## 上传后操作

1. 将视频文件放入本目录。
2. 运行 `python3 deploy_to_server.py` 部署。
3. 用 `curl http://116.62.167.194/` 确认上线。
4. 如需备份，执行 `git add videos/ && git commit -m "add videos" && git push origin main`。
