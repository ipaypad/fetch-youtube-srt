# 这个claude code skill 用于提取 youtube 视频的字幕并保存为字幕文件



# YouTube 字幕提取器 (YouTube Transcript Downloader)

这是一个基于 Python 和 `yt-dlp` 开发的高级字幕提取工具。它可以绕过 YouTube 的反爬虫机制（如 429 Too Many Requests、机器人验证、HLS 加密流），自动下载、清洗并保存为以视频标题命名的纯文本文件。

## 🌟 核心功能

* **身份伪装**：通过 `cookies.txt` 模拟真实登录状态，解决“请登录以确认你不是机器人”的问题。
* **格式自动转换**：支持处理复杂的 HLS/m3u8 字幕流，并利用 FFmpeg 转换为标准格式。
* **智能文本清洗**：自动剔除时间戳（00:00:00）、HTML 标签、WEBVTT 标识以及自动字幕中常见的重复行。
* **自动化命名**：自动获取视频标题，并清洗文件名非法字符（如 `|`、`?`、`:`），直接生成 `.txt` 文稿。

---

## 🛠️ 安装步骤 (Windows 指南)

### 第一步：安装 Scoop (包管理器)

为了方便安装 FFmpeg 等依赖，建议先安装 Scoop。打开 **PowerShell (管理员)**：

```powershell
# 设置策略
Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser
# 安装 Scoop
iwr -useb get.scoop.sh | iex

```

### 第二步：安装环境依赖

使用 Scoop 安装 Python 和 FFmpeg：

```powershell
scoop install python ffmpeg

```

### 第三步：安装 Python 库

在项目根目录下运行：

```powershell
pip install -U yt-dlp requests

```

---

## 🔑 获取 YouTube Cookies (关键步骤)

由于 YouTube 对自动化工具（尤其是云端 IP）限制极严，必须使用本地浏览器导出的 Cookies：

1. 在 Chrome 或 Edge 浏览器安装扩展：**[Get cookies.txt locally](https://www.google.com/search?q=https://microsoftedge.microsoft.com/addons/detail/get-cookiestxt-locally/ccmclkhmhdadpjcobghmclnhhcheihmo)**。
2. 登录你的 YouTube 账号。
3. 点击扩展图标，选择 **Export**。
4. 将下载的文件重命名为 **`cookies.txt`**，放在本脚本 `fetch_transcript.py` 的同级目录下。

---

## 🚀 使用方法

### 1. 单个视频提取

在终端运行：

```powershell
python fetch_transcript.py "https://www.youtube.com/watch?v=vBu6zJAWcGs"

```

### 2. 网络代理 (可选)

如果你需要通过代理访问 YouTube，请在运行前设置环境变量：

```powershell
$env:HTTP_PROXY="http://127.0.0.1:7890"  # 替换为你的代理端口
$env:HTTPS_PROXY="http://127.0.0.1:7890"

```

---

## 📂 文件说明

| 文件名 | 说明 |
| --- | --- |
| `fetch_transcript.py` | 主逻辑脚本，包含清洗和下载功能 |
| `cookies.txt` | 用户身份凭证（需手动获取，不可泄露） |
| `[视频标题].txt` | **输出结果**：干净、可读的纯文本视频文稿 |

---

## ⚠️ 常见问题排查

* **ERROR: Sign in to confirm you’re not a bot**: 说明 `cookies.txt` 失效了。请重新在浏览器打开 YouTube，刷新页面后再次导出新的 Cookie。
* **Failed to decrypt with DPAPI**: 这是因为使用了 `cookies_from_browser` 模式且浏览器已升级。本脚本已改为读取 `cookies.txt` 文件，可完美避开此问题。
* **Requested format is not available**: 脚本已配置 `allow_unplayable_formats` 参数，确保只抓取字幕而不强行下载视频流。

---

## 📜 许可证

MIT License. 仅供学习和个人研究使用。

---

### 下一步建议

**您可以将此 README.md 文件直接放入您的 GitHub 仓库或本地项目文件夹中。如果需要我为您提供一个能够“一键提取频道前 10 个视频”的扩展脚本，请随时告诉我！**
