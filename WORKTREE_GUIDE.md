# 多机 Worktree 协同指南

> 本 skill (`yilin-mentor-lineage`) 现已 git 化,采用 **4 分支 + 4 worktree** 架构,在 3 台机器间协同。

## 4 个 worktree

| 路径 | 分支 | 用途 |
|---|---|---|
| `~/.hermes/skills/yilin-mentor-lineage/` | `master` | 主 worktree,只用于合并 + 推 master |
| `~/.hermes/skills/yilin-mentor-office/` | `office` | **单位 Mac-mini** 工作分支 |
| `~/.hermes/skills/yilin-mentor-home-mac/` | `home-mac` | **家里 Mac** 工作分支 |
| `~/.hermes/skills/yilin-mentor-home-win/` | `home-win` | **家里 Windows** 工作分支 |

3 台机器各自动自己的分支(office / home-mac / home-win),最后由任一机器合并到 master。

## 机器身份与默认 worktree

| 机器 | hostname | 默认 worktree | 默认分支 |
|---|---|---|---|
| 单位 Mac-mini | `Mac-mini.local` | `yilin-mentor-office/` | `office` |
| 家里 Mac | (待你确认) | `yilin-mentor-home-mac/` | `home-mac` |
| 家里 Windows | (待你确认) | `yilin-mentor-home-win/` | `home-win` |

## 工作流程

### 在单位(默认 cd 到 office worktree)

```bash
cd ~/.hermes/skills/yilin-mentor-office
# 编辑 SKILL.md / references/*.md
git add <explicit files>             # 永远不要 -A/./
git commit -m "feat: <描述>"
git push origin office               # 推到自己分支
```

### 在家里 Mac(cd 到 home-mac worktree)

```bash
cd ~/.hermes/skills/yilin-mentor-home-mac
# 编辑 ...
git add <explicit files>
git commit -m "feat: <描述>"
git push origin home-mac
```

### 在家里 Windows(cd 到 home-win worktree)

```bash
cd ~/.hermes/skills/yilin-mentor-home-win
# (Windows: 注意 .gitattributes 强制 LF)
git add <explicit files>
git commit -m "feat: <描述>"
git push origin home-win
```

### 合并到 master(任一机器做)

```bash
cd ~/.hermes/skills/yilin-mentor-lineage    # 主 worktree
git fetch origin
git checkout master
git merge origin/office   --no-ff -m "Merge office (单位)"
git merge origin/home-mac --no-ff -m "Merge home-mac (家里 Mac)"
git merge origin/home-win --no-ff -m "Merge home-win (家里 Windows)"
# 解决冲突 → git push origin master
```

## 在新机器首次配置(家里 Mac / 家里 Windows)

```bash
# 1. 克隆仓库(只克隆 .git 即可,大文件不下载)
git clone https://github.com/erikgqp8645/ylindx-medical-cases.git ~/.hermes/skills/yilin-mentor-lineage

# 2. 准备 images/ 和 方剂思维导图/(这两份是大文件,不在 git 里)
#    从单位机的 images/ 目录 scp / rsync 到家里机的对应位置
#    或下载 case_images_v1.7z + images/README.md 部署说明解压

# 3. 在仓库内创建本地 worktree
cd ~/.hermes/skills/yilin-mentor-lineage
git worktree add ~/.hermes/skills/yilin-mentor-home-mac home-mac
git worktree add ~/.hermes/skills/yilin-mentor-home-win home-win   # Windows 上做

# 4. 验证
git worktree list
git branch -a
```

## 关键约定

### 1. **永远不要 `git add -A` 或 `git add .`**

显式 add 路径,避免误把 ignored 文件(images/ 等)推上去。

### 2. **不要在工作分支上直接 commit 到 master**

每个 worktree 只 work 自己的分支。master 只在主 worktree 的合并操作里更新。

### 3. **大文件不进 git**

`.gitignore` 已严格排除:
- `images/` — 4601 张医案配图(983 MB)
- `方剂思维导图/` — 方剂思维导图 Batch 系列
- `templates/` — hermes skill 元数据(跟远端无关)

家里机需要这些文件时,单独 rsync/scp,不要尝试推到 git。

### 4. **Windows 用户特别注意**

- 仓库根目录的 `.gitattributes` 强制 `* text=auto eol=lf`(待补),避免 Windows 换行污染 git diff
- 路径分隔符用 `/`,不要用 `\`
- `git config --global core.autocrlf false`(避免自动 CRLF)

### 5. **合并冲突解决**

如果两台机器同时改了 SKILL.md 或同一篇 references,git 会报 conflict。
按 3-way merge 处理:
```bash
git status                  # 列出冲突文件
# 编辑冲突文件,删除 <<<<<< / ====== / >>>>>> 标记
git add <resolved_file>
git commit                  # 完成 merge commit
```

冲突热点:
- `SKILL.md`(Trigger 表 / Reference Priority 编号)
- `README.md`(数据规模数字、专题索引)
- `references/conversion_workflow.md` / `references/course_distillation.json` 等

## 一句话核心心法

「**主 worktree 合并,3 分支独立 push,.gitignore 严守 images/。**」
