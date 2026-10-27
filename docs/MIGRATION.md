# 迁移调研与游戏清单

## 调研结论

- 来源：https://gitee.com/manxingjiang/www.wouldplay.cn。
- 基准快照：`15d90e52f5f0308ecf5e800799e78df94abefe76`，上游最后提交日期为 2024-03-19；调研日期为 2026-10-27。
- 上游包含 2,246 个文件，约 84.6 MiB，`yxmb/` 下共 75 个游戏目录。编号不连续，缺少的 1、11、15、46 等编号不是本次迁移遗漏。
- HTML / JavaScript / CSS 静态站点；大厅使用 Bootstrap、jQuery 和 iframe，各游戏自行加载 Canvas、DOM 或 WebGL 实现。没有统一构建系统、后端、数据库或自动化测试。
- 75 款游戏全部保留，另保留黑客模拟器、罗盘时钟与时间刻度作品。没有重新编写游戏规则或统一更换游戏框架。
- 上游根许可证为 Apache-2.0，作者说明包含网络收集源码，文件内第三方声明与素材权利需分别遵循。

## 本次迁移调整

1. 创建 `kerwin1727/wouldplay-games` 公开仓库，以文件快照新建独立历史，不导入上游提交。
2. 仓库 description 和 homepage 均设为 `https://game.haisiplus.cn`，README 提供直接访问链接。
3. 使用 Cloudflare Workers Static Assets，在 `game.haisiplus.cn` 提供 HTTPS 服务，保留全部游戏目录和页面路径。
4. 大厅返回链接改为本站游戏列表；展示上游来源和 GitHub 链接，移除不属于新站点的原备案展示。
5. 移除大厅、黑客模拟器和月饼活动页的原站点统计入口，以及一笔连珠中缺失或内容为 HTML 错误页的统计脚本引用。
6. 大厅背景指向上游实际存在的图片；字体使用本机字体回退，避免请求上游未提交的字体文件。
7. 见缝插口红入口页仅在实际游戏页加载游戏控制脚本，避免入口页缺少游戏节点时报错；兔子吃月饼在微信分享 API 不存在时跳过分享初始化。
8. 从一笔连珠已有资源目录补齐同一游戏其他目录下缺失的图片路径，保留其余原文件。
9. 修正植物大战僵尸、2048 中文版和图像之谜拼图资源路径的大小写，使其能在区分大小写的线上环境加载；根路径在内部转到 `index.html`。
10. 新仓库和部署排除上游遗留的 SVN 元数据、FrontPage 元数据、IDE 缓存及编译缓存，不导入其中的历史记录。

## 验证范围与原版限制

迁移时使用 Chromium 逐一打开全部 75 个游戏入口，并检查大厅、黑客模拟器和附加作品。检查包含页面 HTTP 状态、初始化脚本错误和实际加载资源；不等于逐款通关测试，也不保证所有游戏适配所有手机。

以下问题在上游快照中已经存在，相关文件全部保留：

| 游戏 | 上游问题 / 使用限制 |
| --- | --- |
| 重力球滚动（33） | 7 个精灵图依赖 `image.noelshack.com`，调研时均返回 404；上游没有这些图片，可能无法开始游戏。 |
| 贪吃蛇 2.0（14） | 3 张背景图没有提交到上游仓库；背景预览会缺图。 |
| 飞机躲避（55） | 背景图 `css/images/bg.png` 缺失。 |
| 中国象棋（65） | `audio/click.wav`、`audio/select.wav` 缺失，相关音效不可用。 |
| 像素小鸟飞行（64）、森林协奏曲（75） | `p2l.jpg` 推广图缺失。 |
| 植物大战僵尸（4） | 原版加载远程 `Process.js` 更新信息，域名连接失败；游戏素材和关卡另在本地。部分音乐采用旧 Flash 格式，现代浏览器无法播放。 |
| 部分旧移动游戏 | 页面加载时尝试自动播放音频，现代浏览器会拦截；需要用户先点击。旧版微信分享、排行榜及更多游戏按钮仍可能跳转原第三方站点。 |
| 变色弹球跳台阶（35）、中国象棋（65）、记忆小游戏（70）、16 宫格翻牌匹配（73） | 部分字体或样式仍由第三方 HTTPS 服务提供，网络状况可能影响外观。 |
| 黑客模拟器 | 原样式引用的 `css/progres.png` 缺失；原脚本有一处访问不存在的 DOM 节点会报错，部分装饰功能可能异常。 |

原有游戏资源缺失与旧浏览器兼容问题不应被描述为已经全部修复。可在后续逐项补充原始授权资源并做完整玩法测试。

## 全部游戏入口

| 编号 | 游戏 | 本地入口 |
| --- | --- | --- |
| 2 | 一个都不能死 | [打开](../yxmb/2/index.html) |
| 3 | 捕鱼达人 | [打开](../yxmb/3/index.html) |
| 4 | 植物大战僵尸 | [打开](../yxmb/4/index.html) |
| 5 | 3D魔方 | [打开](../yxmb/5/index.html) |
| 6 | 青蛙吃苍蝇 | [打开](../yxmb/6/index.html) |
| 7 | 蜘蛛纸牌 | [打开](../yxmb/7/index.html) |
| 8 | 贪吃蛇 | [打开](../yxmb/8/index.html) |
| 9 | 水果消除 | [打开](../yxmb/9/index.html) |
| 10 | 2048中文版 | [打开](../yxmb/10/index.html) |
| 12 | 飞机大战 | [打开](../yxmb/12/index.html) |
| 13 | 跑酷小游戏 | [打开](../yxmb/13/index.html) |
| 14 | 贪吃蛇2.0 | [打开](../yxmb/14/index.html) |
| 16 | 激流勇进 | [打开](../yxmb/16/index.html) |
| 17 | 天天消消乐 | [打开](../yxmb/17/index.html) |
| 18 | 别踩白块 | [打开](../yxmb/18/index.html) |
| 19 | 线条生存 | [打开](../yxmb/19/index.html) |
| 20 | 打砖块射击 | [打开](../yxmb/20/index.html) |
| 21 | 保卫星球射击 | [打开](../yxmb/21/index.html) |
| 22 | 吃豆人 | [打开](../yxmb/22/index.html) |
| 23 | 开心消消乐 | [打开](../yxmb/23/index.html) |
| 24 | 俄罗斯方块 | [打开](../yxmb/24/index.html) |
| 25 | 2048方块版 | [打开](../yxmb/25/index.html) |
| 26 | 看图猜词 | [打开](../yxmb/26/index.html) |
| 27 | 弹球打砖块 | [打开](../yxmb/27/index.html) |
| 28 | 小方块回家 | [打开](../yxmb/28/index.html) |
| 29 | 双人五子棋 | [打开](../yxmb/29/index.html) |
| 30 | 射箭小游戏 | [打开](../yxmb/30/index.html) |
| 31 | 飞机大战2.0 | [打开](../yxmb/31/index.html) |
| 32 | 简单闯关游戏 | [打开](../yxmb/32/index.html) |
| 33 | 重力球滚动 | [打开](../yxmb/33/index.html) |
| 34 | 头像迷阵消除 | [打开](../yxmb/34/index.html) |
| 35 | 变色弹球跳台阶 | [打开](../yxmb/35/index.html) |
| 36 | 最强眼力 | [打开](../yxmb/36/index.html) |
| 37 | 俄罗斯方块2.0 | [打开](../yxmb/37/index.html) |
| 38 | 双人五子棋2.0 | [打开](../yxmb/38/index.html) |
| 39 | 小人推箱子 | [打开](../yxmb/39/index.html) |
| 40 | 经典扫雷 | [打开](../yxmb/40/index.html) |
| 41 | 英雄宝石块消消乐 | [打开](../yxmb/41/index.html) |
| 42 | 赛车游戏 | [打开](../yxmb/42/index.html) |
| 43 | 大家来找茬 | [打开](../yxmb/43/index.html) |
| 44 | 经典扫雷2.0 | [打开](../yxmb/44/index.html) |
| 45 | 锅打灰太狼 | [打开](../yxmb/45/index.html) |
| 47 | 兔子吃月饼 | [打开](../yxmb/47/index.html) |
| 48 | 接金币 | [打开](../yxmb/48/index.html) |
| 49 | 灌篮高手 | [打开](../yxmb/49/index.html) |
| 50 | 疯狂打企鹅 | [打开](../yxmb/50/index.html) |
| 51 | 吃月饼大赛 | [打开](../yxmb/51/index.html) |
| 52 | 坦克大战 | [打开](../yxmb/52/index.html) |
| 53 | 图像之谜拼图 | [打开](../yxmb/53/index.html) |
| 54 | 消除QQ表情 | [打开](../yxmb/54/index.html) |
| 55 | 飞机躲避 | [打开](../yxmb/55/index.html) |
| 56 | 3D熊出没 | [打开](../yxmb/56/index.html) |
| 57 | 3D拼图魔方 | [打开](../yxmb/57/index.html) |
| 58 | 3D拳王拳击 | [打开](../yxmb/58/index.html) |
| 59 | 围住神经猫 | [打开](../yxmb/59/index.html) |
| 60 | 2048军旗版 | [打开](../yxmb/60/index.html) |
| 61 | 打地鼠 | [打开](../yxmb/61/index.html) |
| 62 | 驴子跳跳 | [打开](../yxmb/62/index.html) |
| 63 | 压扁像素小鸟 | [打开](../yxmb/63/index.html) |
| 64 | 像素小鸟飞行 | [打开](../yxmb/64/index.html) |
| 65 | 中国象棋 | [打开](../yxmb/65/index.html) |
| 66 | 经典飞机大战 | [打开](../yxmb/66/index.html) |
| 67 | 简约打地鼠 | [打开](../yxmb/67/index.html) |
| 68 | 切积木 | [打开](../yxmb/68/index.html) |
| 69 | 见缝插口红 | [打开](../yxmb/69/index.html) |
| 70 | 记忆小游戏 | [打开](../yxmb/70/index.html) |
| 71 | 看图猜词2.0 | [打开](../yxmb/71/index.html) |
| 72 | 萝卜载兔子飞行 | [打开](../yxmb/72/index.html) |
| 73 | 16宫格翻牌匹配 | [打开](../yxmb/73/index.html) |
| 74 | 一笔连珠 | [打开](../yxmb/74/index.html) |
| 75 | 森林协奏曲 | [打开](../yxmb/75/index.html) |
| 76 | 斗地主 | [打开](../yxmb/76/index.html) |
| 77 | 飞机加减速 | [打开](../yxmb/77/index.html) |
| 78 | 响应式翻牌 | [打开](../yxmb/78/index.html) |
| 79 | 天降红包雨 | [打开](../yxmb/79/index.html) |

## 其他作品

- [黑客模拟器](../hacker/index.html)
- [罗盘时钟](../compasstime/time.html)
- [罗盘其他样式](../compasstime/compass.html)
- [时钟其他样式](../compasstime/index.html)
- [时间刻度](../time/index.html)

