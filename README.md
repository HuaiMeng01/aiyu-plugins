# 爱语插件源

一份给「爱语」用的插件索引仓库。装上 `pkg_hub` 插件后，在聊天里就能浏览、审查、取回这里的插件包。

## 在爱语里用

**第一次（引导安装）**

1. 下载 `zips/pkg_hub_v1.1.1.zip`
2. 爱语 → 插件管理 → 本地导入 → 选中它
3. 权限全给：`register_instruction`、`inject_system_prompt`、`access_network`

**之后（全部在聊天里）**

```
原样输出 <pkg:source HuaiMeng01/aiyu-plugins>
原样输出 <pkg:list>
原样输出 <pkg:info 爱心代码>
原样输出 <pkg:url 爱心代码>
```

`<pkg:url>` 给出的是套了可用代理的下载直链，拿到后用「插件管理 → 本地导入」装上。

指令没反应或报格式错误时，发 `<pkg:diag>` 自检：它会把「原生返回 → 解析后源 → 候选地址 → 实际拉取」摊开。

## 目录结构

```
.
├── plugins.json          # 索引，插件只读这一个文件
└── zips/
    ├── pkg_hub_v1.1.1.zip
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

国内直连 `raw.githubusercontent.com` 常常不通，插件内置了三级回退：**GitHub 代理 → jsDelivr → 直连**，并记住上次成功的通道。代理是否可用因网络而异，可在聊天里发 `<pkg:proxy test>` 自查。

## 校验

`plugins.json` 里每条都带 `sha256` 与 `bytes`。想手工核对：

```bash
sha256sum zips/aiyu_heart_v1.1.0.zip
```
