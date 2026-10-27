# 好玩有趣的事儿 · 小游戏平台

在线游玩：**<https://game.haisiplus.cn>**

从 [Gitee 原仓库](https://gitee.com/manxingjiang/www.wouldplay.cn) 迁移的纯 HTML / JavaScript 小游戏集合。包含全部 **75 款游戏**、黑客模拟器、罗盘时钟和时间刻度作品，无需后端、数据库或编译。

## 本地运行

在项目根目录启动任意静态文件服务，例如：

```sh
python -m http.server 8080
```

打开 <http://localhost:8080>。部分游戏使用资源加载和音频，需要通过 HTTP 服务访问；声音通常需要点击后才能播放。

## 部署

本项目使用 Cloudflare Workers Static Assets，站点目录为仓库根目录，配置见 `wrangler.jsonc`。`.assetsignore` 排除 Git 数据、工具配置与文档。

```sh
npx wrangler@4.149.0 login
npx wrangler@4.149.0 deploy
```

部署到自己的账号时，修改 `account_id`、`name` 与 `routes`。正式域名为 <https://game.haisiplus.cn>，保留每款游戏原有的 `yxmb/<编号>/index.html` 路径。也可把静态文件部署到其他支持 HTTPS 的网站根目录。

推送 GitHub 不会自动发布网站；更新后需重新部署。

## 游戏与目录

- `yxmb/`：75 款游戏，包括植物大战僵尸、捕鱼达人、3D 魔方、2048、贪吃蛇、俄罗斯方块、五子棋、中国象棋、斗地主等。
- `link/`：全部游戏入口、益智 / 动作 / 射击 / 消除 / 休闲 / 棋牌分类及其他作品。
- `hacker/`：黑客模拟器。
- `compasstime/`、`time/`：时钟与时间刻度作品。
- `css/`、`js/`、`images/`：平台公共资源。
- [迁移调研与游戏清单](docs/MIGRATION.md)：来源、技术结构、迁移范围、游戏入口和验证情况。

## 来源与许可

原项目作者 / 贡献者：中庸之圣（Gitee：manxingjiang）。原项目说明源码来自源码之家、A5 源码及个人程序。

本次迁移以原仓库 `15d90e52f5f0308ecf5e800799e78df94abefe76` 的文件快照为基础，新建独立 Git 历史；原仓库的 [Apache-2.0 许可证](LICENSE) 和文件内第三方声明保持保留。迁移调整记录见 [迁移说明](docs/MIGRATION.md)。

游戏、图片、音乐及第三方库可能另有各自权利声明，仓库根许可证不能替代这些素材的原始授权；商业使用前请逐项核实。

