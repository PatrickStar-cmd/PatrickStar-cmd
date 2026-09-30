# 个人主页维护说明

本仓库的 `README.md` 会显示在 GitHub 个人主页。

## 修改自我介绍

打开 `assets/intro.svg`，修改文件底部的四段 `<text>` 文字并提交。
文字按四句循环显示；渐变颜色由顶部 `intro-gradient` 的 `<stop>` 设置控制。
修改后也应更新 SVG 的 `<desc>` 和 README 中图片的 `alt`，使备用介绍保持一致。

## 修改技术和游戏图标

编辑 `README.md` 中的 `<img>` 标签。标签排列顺序就是主页图标顺序。
MATLAB 使用仓库内的 `assets/matlab-badge.svg`；其余徽标使用 Shields.io。

## 更新贡献贪吃蛇

配置文件为 `.github/workflows/snake.yml`。
当前每天 UTC 00:00（北京时间 08:00）自动生成浅色和深色 SVG，提交至 `output` 分支。
定时任务可能延迟，新增贡献会在下次成功生成后体现在动画中。

需要立即更新时，打开仓库 Actions → Snake → Run workflow，选择 `main` 并运行。
运行成功后，检查 `output` 分支中的 `github-snake.svg` 和 `github-snake-dark.svg`。
如果主页暂时显示旧图，可刷新页面并等待图片缓存更新。

私有贡献是否包含在动画中，取决于 GitHub 个人主页的私有贡献展示设置。
开启路径：个人主页贡献日历上方的 Contribution settings → Private contributions。
这个设置只展示贡献日期和数量，不公开私有仓库内容。

动画播放时，蛇会吃掉绿色格子；比较贡献图时，应观察动画刚开始的一轮。

### 贡献格子不一致时如何排查

1. 先检查 GitHub 贡献日历是否已经包含目标日期的贡献；需要统计私有贡献时，确认已开启上述设置。
2. 查看 Actions 中最近一次 Snake 的运行时间和结果。日历有新贡献，不代表已有 SVG 会立即改变；
   等待每日生成，或在 `main` 上手动运行一次。
3. 运行成功后，在 `output` 分支查看对应 SVG 的最近提交。
   如果生成文件仍是旧版本，打开该次运行的 Generate contribution snake 和 Publish SVGs 日志查找原因。
4. 如果 `output` 分支已有新文件而主页仍显示旧图，检查 README 引用的分支及浅色、深色文件名，
   再等待 GitHub 图片代理或原始文件缓存更新。深色模式需要单独核对 `github-snake-dark.svg`。

仓库里的生成文件和主页上的缓存图片是两个检查位置；重复刷新主页不能重新生成贡献动画。

## 文件位置

- `README.md`：主页布局和图片引用。
- `assets/intro.svg`：渐变自我介绍动画。
- `assets/matlab-badge.svg`：MATLAB 徽标。
- `.github/workflows/snake.yml`：贪吃蛇生成与发布流程。
- `output` 分支：工作流生成的贡献动画。

## 在 GitHub 网页上管理文件

GitHub 使用文件路径表示目录，不会保存空目录。
在仓库页面选择 Add file → Create new file，在文件名中输入 `目录/子目录/文件名`，
例如 `docs/notes/example.md`。填写内容并提交后，会同时创建所需目录和文件。

编辑现有文件时，打开文件并点击铅笔图标；删除文件时，打开文件，
在文件操作菜单中选择 Delete file，再提交删除。删除目录中最后一个文件后，目录也会消失。
已经提交的文件可以从 Git 历史找回；未提交的编辑内容不在历史中。

主页介绍可以直接通过以下链接编辑：
[编辑 intro.svg](https://github.com/PatrickStar-cmd/PatrickStar-cmd/edit/main/assets/intro.svg)。

## 本地仓库

主页和定时任务在 GitHub 上运行，不需要本地电脑一直开机。
删除本地副本前，请确认要保留的修改已提交并推送，另外备份未跟踪、被忽略的本地文件。
之后可以重新克隆本仓库。
