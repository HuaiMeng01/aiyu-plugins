# 爱语插件源

一份给「爱语」用的插件索引仓库。装上 `pkg_hub` 插件后，在聊天里就能浏览、审查、取回这里的插件包。

## 在爱语里用

**第一次（引导安装）**

1. 下载 `zips/pkg_hub_v2.1.2.zip`
2. 爱语 → 插件管理 → 本地导入 → 选中它
3. 权限全给：`register_instruction`、`inject_system_prompt`、`access_network`、`read_app_files`、`write_app_files`

**之后：两种装法**

*页面装*：扩展 → 插件源 → 打开 → 选加速通道（默认自动）→ 粘贴 GitHub 链接（`owner/repo` 或 `plugins.json` 地址）→ 载入 → 选插件 → 安装。装前会列出权限。

*聊天装*：

```
原样输出 <pkg:install 爱心代码>
原样输出 <pkg:install https://…/xxx.zip>
原样输出 <pkg:installed>
```

也可以直接说「帮我装一下爱心代码」，AI 会自己发指令。

装完**重启爱语**，到「扩展 → 模块」即可看到。

## 目录结构

```
.
├── plugins.json          # 索引，插件只读这一个文件
└── zips/
    ├── pkg_hub_v2.1.2.zip
    ├── aiyu_heart_v1.1.0.zip
    ├── aiyu_image_downloader_v1.0.0.zip
    └── aiyu_token_viewer_v2.2.1.zip
```

## 加一个插件

1. 把 zip 放进 `zips/`
2. 在 `plugins.json` 的 `plugins` 数组里追加一条：

```json
{
  "id": "my_plugin",
  "name": "我的插件",
  "version": "1.0.0",
  "author": "你的名字",
  "description": "一句话说明它做什么",
  "zip": "zips/my_plugin_v1.0.0.zip",
  "permissions": ["register_instruction"]
}
```

3. 提交推送。`zip` 用相对路径，插件会按索引地址自动补全，不用写死域名。

## 关于权限

装第三方插件等于执行别人的代码。这几项要格外小心：

| 权限 | 意味着 |
|---|---|
| `read_chat_history` | 能读你所有聊天记录 |
| `read_memory` / `write_memory` | 能读写记忆库 |
| `inject_system_prompt` | 能改 AI 的系统提示词，从而改变角色行为 |
| `write_app_files` | 能往应用私有目录写文件 |

`<pkg:info>` 会把这些翻译成人话，装之前先看一眼。

## 关于访问

国内直连 `raw.githubusercontent.com` 常常不通。打开「插件源」页面，在**加速通道**那一栏点一个地址即可（自动 / gh-proxy / dpik / edgeone / hk / jsDelivr / 直连），点「测速」会显示每个通道的延迟，选择会被记住。聊天里不需要也不应该管这些，AI 只用 `<pkg:install>` 下载安装。

## 校验

`plugins.json` 里每条都带 `sha256` 与 `bytes`。想手工核对：

```bash
sha256sum zips/aiyu_heart_v1.1.0.zip
```
