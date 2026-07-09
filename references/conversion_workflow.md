# lineage-skill 转换流程

## 概述
将医林独啸斋的456篇markdown文章转换为lineage-skill可搜索的课程格式。

## 环境
- lineage-skill仓库: `/Users/applemima1111/AiCoding/lineage-skill/`
- 源文章目录: `/Users/applemima1111/AiCoding/医林独啸斋/markdown/` (456个md文件)
- 输出: `courses/医林独啸斋/` (course_package.json, full_transcript.md, course_digest.md, lesson_index.json)
- 安装位置: `~/.hermes/skills/yilin-mentor-lineage/`

## 关键步骤

### 1. 环境准备
```bash
pip3 install --break-system-packages python-dotenv openai
```

### 2. 配置API
lineage-skill的`.env`需要`LINEAGE_TEXT_API_KEY`，从`~/.hermes/.env`的`DEEPSEEK_API_KEY`复制。

### 3. 自定义转换器
标准`distill_course.py`期望`transcripts/`目录下的JSON格式，不兼容markdown。
需要自定义转换器: `scripts/convert_yilin_to_lineage.py`

### 4. 构建课程包
```bash
cd /Users/applemima1111/AiCoding/lineage-skill
python3 scripts/convert_yilin_to_lineage.py
```

### 5. 生成skill
```bash
python3 scripts/build_course_skill.py --mode mentor --source courses/医林独啸斋/
```

### 6. 安装skill
将生成的skill复制到`~/.hermes/skills/yilin-mentor-lineage/`

## 坑
- macOS Homebrew Python需要`--break-system-packages`标志
- `course_package.json`约10MB，`full_transcript.md`约9.5MB，加载时注意上下文窗口
- md文件中的图片是微信外部URL，不需要本地存储
- 医林独啸斋原目录有`cases/`、`封面/`、`视频/`等非markdown目录，可安全删除（md文件不引用本地图片）
