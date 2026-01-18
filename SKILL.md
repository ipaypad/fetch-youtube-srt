---
name: fetch-youtube-srt
description: "通过执行本地 Python 脚本获取 YouTube 视频的转录文本。该工具仅需一个视频 URL 即可提取完整的对话内容，适用于视频总结、内容分析和翻译任务。"
---

<objective>
使用指定的 Python 脚本 `fetch_transcript.py`，通过完整的 YouTube 视频 URL 直接获取其字幕/转录文本。
</objective>

<quick_start>
**核心指令：**
在终端中执行以下命令来获取特定视频的转录内容：

```bash
python .\scripts\fetch_transcript.py "http://www.youtube.com/watch?v=6WjdqxcEjR8"
```
</quick_start>

<core_operations>

1. 提取视频转录文本 该 Skill 简化为单一接口调用，通过传递 URL 参数来触发脚本逻辑。

Bash

# 格式: python .\scripts\fetch_transcript.py <YOUTUBE_URL>
python .\scripts\fetch_transcript.py [http://www.youtube.com/watch?v=6WjdqxcEjR8](http://www.youtube.com/watch?v=6WjdqxcEjR8)
2. 结合 Claude 进行后续处理 获取文本后，通常用于以下场景：

内容总结：要求 Claude 总结获取到的文本内容。

关键点提取：从视频文本中提炼核心观点。

语言翻译：将获取的文本翻译成其他目标语言。

</core_operations>

<usage_examples>
用户提示词示例：

"运行 fetch_transcript.py 帮我提取这个视频的内容：http://www.youtube.com/watch?v=6WjdqxcEjR8"

"执行脚本获取该链接的字幕并总结摘要：http://www.youtube.com/watch?v=6WjdqxcEjR8"

"调用 python .\fetch_transcript.py 处理视频，然后将其翻译成中文。"

</usage_examples>


<error_handling> 若脚本执行失败，常见错误包括：

TranscriptsDisabled: 该视频的字幕功能被禁用。

VideoUnavailable: 视频为私有、已删除或不存在。

NoTranscriptFound: 未找到所请求语言的转录文本。

InvalidURL: 提供的 YouTube 链接格式不正确。 
</error_handling>

<success_criteria>

脚本成功解析 URL 并获取视频转录数据。

转录文本完整输出到控制台。

Claude 能够基于输出内容进行后续的分析或总结任务。 
</success_criteria>