---
name: visual-understanding
description: 图片视觉理解技能。当用户发送图片并希望了解图片内容、分析图片、提取信息时使用此技能。支持截图、照片、扫描件等各类图片，能识别文字、物体、场景、人物等所有视觉元素。触发场景：(1) 用户发送图片 (2) 用户问图片里有什么 (3) 用户要求分析图片内容 (4) 用户说"看看这张图"等类似表达
---

# Visual Understanding Skill · 图片视觉理解

## 核心工具

**`images_understand`** — 批量图片理解工具

支持 jpeg、png、gif、webp，最多一次传 20 张，返回纯文本分析结果。

## 标准工作流

### Step 1：保存图片

收到图片时，将其复制到 `/workspace/` 目录：

```python
# 图片通常在 /root/.openclaw/media/inbound/{uuid}.{ext}
# 复制到 workspace
cp /root/.openclaw/media/inbound/{filename}.{ext} /workspace/image.jpg
```

### Step 2：调用 images_understand

```python
images_understand(
  image_info=[
    {
      "file": "/workspace/image.jpg",
      "prompt": "请详细描述这张图片的内容，包括所有文字、场景、物品、人物等细节。"
    }
  ]
)
```

### Step 3：验证输出（如需要）

如果结果不明确，可用 `images_understand` 再次分析或追加 prompt。

## 常用 Prompt 模板

### 通用描述
```
请详细描述这张图片的全部内容，包括所有文字、场景、物品、人物等细节。
```

### 提取关键信息（卡片/截图/文档）
```
请提取图片中所有可见的文字内容和关键信息。
```

### 评估/判断（产品/穿着/场景）
```
请详细描述图片中的人物/物品/场景，并评估是否适合[具体场景]。
```

### 识别并翻译文字
```
请识别图片中的所有文字内容，如果是英文或其他语言请翻译成中文。
```

## 注意事项

- ⚠️ **不要用 `read` 工具读取图片文件** — 某些模型不支持 vision，分析会失败
- ✅ **始终用 `images_understand` 处理图片**
- ⚠️ GIF 只分析第一帧
- ✅ 图片文件需先复制到 `/workspace/` 目录，工具才能访问
- ⚠️ 图片文件不要超过 50MB

## 常见问题

**图片读取失败**
→ 确认文件已复制到 `/workspace/`，再重试

**结果不准确**
→ 调整 prompt，增加具体要求，如"请重点关注XXX"

**文件路径含中文**
→ 文件名不要含中文路径
