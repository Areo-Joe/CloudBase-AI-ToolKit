# 常见问题 FAQ

## 🌟 选择 CloudBase 的原因

### 为什么选择 CloudBase？

- **⚡ 极速部署**：国内节点,访问速度比海外更快
- **🛡️ 稳定可靠**：330 万开发者选择的 Serverless 平台
- **🔧 开发友好**：专为AI时代设计的全栈平台，支持自动环境配置
- **💰 成本优化**：Serverless 架构更具弹性，新用户开发期间可以免费体验

## 🚀 开始使用

### 我是新用户，如何快速开始？

1. 安装支持的 AI 开发工具（如 Cursor、WindSurf 等）
2. 在腾讯云开发控制台开通环境（新用户免费）
3. 下载项目模板或在现有项目中配置 MCP
4. 对 AI 说"登录云开发"开始开发

### 支持哪些 AI 开发工具？
支持 Cursor、WindSurf、CodeBuddy、CLINE、GitHub Copilot、Claude Code、Gemini CLI、OpenAI Codex CLI、OpenCode、Trae、通义灵码、RooCode、文心快码、Augment Code、Qwen Code 等主流 AI 开发工具。

## 🛠️ 技术问题


### 已有项目如何集成本模板和规则体系？

如果你已经有自己的项目，只需在配置好 MCP 后，只需要对 AI 说 "在当前项目中下载云开发 AI 规则"，即可一键下载并补全 AI 编辑器规则配置到当前项目目录，无需手动操作。

---

### 如何获取云开发环境 ID？

1. 访问 [腾讯云开发控制台](https://tcb.cloud.tencent.com/dev)开通环境，新用户可以免费开通体验
2. 在控制台「概览」页面右侧获取 **环境ID**  
   （后续部署需要此 ID）

---

### 如何更新 CloudBase AI ToolKit？

**更新 AI 规则**

如果你想在现有项目中更新到最新的云开发 AI 规则，只需对 AI 说：

```
下载云开发 AI 规则在当前项目中更新 rules
```

AI 会自动下载并更新最新的规则配置到你的项目目录。

**更新 MCP 工具**

当有新版本的 MCP 工具发布时，你可以通过以下方式更新：

1. **自动更新（推荐）**：在你的 AI 开发工具的 MCP 列表中，找到 cloudbase-mcp 并重新启用或刷新 MCP 列表即可自动安装最新版本

2. **手动更新**：如果自动更新不成功，可以先禁用再重新启用 cloudbase-mcp，或者重启你的 AI IDE

**注意事项**：
- MCP 配置中使用了 `@latest` 标签，通常会自动获取最新版本
- 如果遇到缓存问题，可以完全重启 AI IDE 后重新启用 MCP
- 建议定期检查更新以获得最新功能和修复

### 如何全局安装 CloudBase AI ToolKit？

如果你希望全局安装 CloudBase AI ToolKit 以避免每次使用 npx 下载，可以使用以下方法：

**1. 全局安装**
```bash
npm i @cloudbase/cloudbase-mcp@latest -g
```

**2. 更新 MCP 配置**
安装完成后，将 MCP 配置中的 `command` 从 `npx` 改为直接使用命令：

```json
{
  "mcpServers": {
    "cloudbase": {
      "command": "cloudbase-mcp"
    }
  }
}
```

**优势：**
- 启动速度更快，无需每次下载
- 避免网络问题导致的启动失败
- 减少 npx 缓存相关问题

**注意事项：**
- 需要手动更新：`npm update @cloudbase/cloudbase-mcp -g`
- 确保全局安装的版本是最新的

---

### MCP 显示工具数量为 0 怎么办？

如果在 AI 开发工具的 MCP 列表中看到 cloudbase-mcp 显示工具数量为 0，可以按以下步骤排查：

**1. 检查环境配置**
- 确保 Node.js 版本为 v18.15.0 及以上
- macOS 用户且使用 nvm 管理 Node.js 的，请务必设置默认 Node 版本为 v18.15.0 及以上，避免不同终端版本不一致导致的问题。
  设置默认版本命令示例：
  ```bash
  nvm alias default 18.15.0
  ```
- 检查网络连接，建议设置 npm 源为腾讯镜像源：
  ```bash
  npm config set registry https://mirrors.cloud.tencent.com/npm/
  ```
- 输入如下命令测试，若无异常报错则为正常启动服务
  ```bash
  npx @cloudbase/cloudbase-mcp@latest
  ```

**2. 清理缓存**
- 清理 npx 缓存（npx 存在缓存 bug 可能导致安装问题）：
  ```bash
  npx clear-npx-cache
  ```

**3. 重新启用 MCP**
- 在 AI 开发工具的 MCP 列表中禁用 cloudbase-mcp
- 重新启用 cloudbase-mcp 或刷新 MCP 列表
- 如果仍有问题，完全重启 AI IDE 后重试

**4. 手动重新安装**
- 如果上述方法无效，可以删除 MCP 配置后重新添加
- 确保使用最新的配置格式

**5. 尝试全局安装**
- 如果 npx 方式持续有问题，可以尝试[全局安装方式](#如何全局安装-cloudbase-ai-toolkit)

**6. 使用 inspector 工具验证 MCP 连接**
- 如果上述方法都无效，可以通过 inspector 工具进一步排查 MCP 是否正常：
  ```bash
  npx @modelcontextprotocol/inspector npx @cloudbase/cloudbase-mcp@latest
  ```
- 命令行会输出类似如下的网址：
  ```
  http://localhost:6274/?MCP_PROXY_AUTH_TOKEN=8fbe0137d3bd77f0181a66a0ced8476283ba2b25927f2d3fd84492dfa1eb2199
  ```
- 用浏览器打开该网址，填写如下信息：
  - **Command** 填写为 `npx`
  - **Arguments** 填写为 `@cloudbase/cloudbase-mcp@latest`
  - 然后点击 **Connect** 进行测试，需要等待安装和连接 MCP Server
- 如果测试 OK，说明 MCP 工具本身连接正常，问题可能出在客户端配置或环境。
- 如果连接失败，可以复制下方红色的错误信息，在 [社区 issue](https://cnb.cool/tencent/cloud/cloudbase/community/-/issues) 提交问题，便于进一步排查。

一般情况下，在 MCP 列表中重新启用或刷新即可正常安装并显示工具。



---

### MCP 配置不生效怎么办？

1. 检查配置格式是否正确
2. 重启 AI IDE
3. 确认 MCP 服务已启用

### Safari 浏览器无法完成授权登录怎么处理？

如果在使用 Safari 浏览器时遇到授权登录问题，建议切换到 Chrome 浏览器进行授权登录。

Safari 浏览器在某些情况下可能存在兼容性问题，影响授权流程的正常进行。Chrome 浏览器对云开发授权流程有更好的支持。

---

### 远程开发环境或服务端如何使用 MCP？

如果你在远程开发环境中工作，或者需要在没有浏览器的服务端环境中直接调用 MCP，无法通过浏览器完成授权登录，可以使用环境变量来配置腾讯云密钥和环境信息。

**配置方法：**

在 MCP 配置中使用 `env` 环境变量来设置认证信息：

```js
{
  "mcpServers": {
    "cloudbase-mcp": {
      "command": "npx",
      "args": ["@cloudbase/cloudbase-mcp@latest"],
      "env": {
        "TENCENTCLOUD_SECRETID": "腾讯云 SecretId",
        "TENCENTCLOUD_SECRETKEY": "腾讯云 SecretKey",
        "TENCENTCLOUD_SESSIONTOKEN": "腾讯云临时密钥Token，如果使用临时密钥才需要传入",
        "CLOUDBASE_ENV_ID": "云开发环境 ID"
      }
    }
  }
}
```

**获取密钥信息：**
- 腾讯云 SecretId 和 SecretKey：在 [腾讯云访问管理控制台](https://console.cloud.tencent.com/cam/capi) 获取
- 云开发环境 ID：在 [腾讯云开发控制台](https://tcb.cloud.tencent.com/dev) 概览页面获取

这种方式特别适用于：
- 远程开发环境（如 GitHub Codespaces、云 IDE 等）
- 服务端自动化脚本
- CI/CD 流水线中的自动化部署

---

### 支持哪些应用类型？

- **Web应用**：现代化前端 + 静态托管
- **微信小程序**：云开发小程序解决方案
- **后端服务**：云数据库 + 无服务器函数+云托管

---

### 开发微信小程序时有什么特别建议？

**推荐开发流程：**

1. **在微信开发者工具中开通云开发环境**
   - 直接在微信开发者工具里开通，确保小程序与云开发环境完美绑定

2. **AI IDE 登录时选择【小程序/公众号】登录**
   - 跳转登录腾讯云云开发时，选择【小程序/公众号】登录
   - 使用你的小程序来登录，而不是腾讯云主账号

这样可以保证权限一致性，避免环境配置问题。

---

### 如何在微信开发者工具中使用 CloudBase AI ToolKit？

CloudBase AI ToolKit 与微信开发者工具可以完美配合使用，提供更高效的开发体验。

#### 方式一：从 AI IDE 开始开发

如果你已经在 AI IDE（如 Cursor、WindSurf、CodeBuddy 等）中开始开发小程序项目：

1. **AI IDE 开发**：在 AI IDE 中使用 CloudBase AI ToolKit 进行代码编写和云开发资源管理
2. **导入微信开发者工具**：在微信开发者工具中导入整个项目文件夹
3. **实时同步**：AI IDE 中的文件变化会实时同步到微信开发者工具
4. **构建预览**：在微信开发者工具中执行构建和预览操作
5. **错误排查**：如果遇到构建或运行错误，可以复制错误信息到 AI IDE 中进行智能排障

**优势：**
- 享受 AI 智能编程的便利
- 利用微信开发者工具的原生调试能力
- 实时预览和真机调试
- 完整的开发工具链

#### 方式二：从微信开发者工具开始

如果你已有微信开发者工具中的小程序项目：

1. **打开项目**：在 AI IDE 中打开现有的小程序项目文件夹
2. **配置 MCP**：参考文档配置 CloudBase MCP 服务
3. **下载 AI 规则**：对 AI 说"下载云开发 AI 规则"获取开发规则
4. **开始 AI 开发**：使用 AI 进行代码编写和云开发资源管理
5. **微信开发者工具预览**：在微信开发者工具中进行实时预览和调试

**工作流程：**
- AI IDE：负责代码编写、云函数开发、数据库设计等
- 微信开发者工具：负责小程序预览、真机调试、性能分析等
- 两者协同工作，发挥各自优势

**注意事项：**
- 确保两个工具打开的是同一个项目文件夹
- 文件保存后会自动同步，无需手动操作
- 建议在 AI IDE 中完成主要开发工作，在微信开发者工具中进行最终测试

---

## 🔄 环境管理

### 如何切换云开发环境？

```
退出云开发
登录云开发
```

### 如何切换腾讯云账号？

如果需要切换到不同的腾讯云账号：

1. **清理本地登录态**：对 AI 说 `退出登录`
2. **浏览器退出登录**：到浏览器里面退出原来登录的腾讯云账号
3. **重新登录**：对 AI 说 `登录云开发`

这样就可以切换到新的腾讯云账号了。

### 如何确认当前环境？

```
查询当前云开发环境信息
```

## 🐛 问题排查

### 部署失败了怎么办？
把完整的错误信息发给 AI：
```
报错了，错误是xxxx
```

### 云函数运行异常如何调试？
让 AI 查看日志并修复：
```
云函数代码运行不符合需求，需求是 xxx，请查看日志和数据进行调试，并进行修复
```



## 💬 技术交流群

遇到问题或想要交流经验？加入我们的技术社区！

### 🔥 微信交流群

<div align="center">
<img src="https://7463-tcb-advanced-a656fc-1257967285.tcb.qcloud.la/mcp/toolkit-qrcode.png" width="200" alt="微信群二维码"/>
<br/>
<i>扫码加入微信技术交流群</i>
</div>

## 技术支持

### 遇到问题如何获取帮助？

1. 查看常见问题 FAQ
2. 在 [GitHub Issues](https://github.com/TencentCloudBase/CloudBase-AI-ToolKit/issues) 提交问题
3. 加入微信技术交流群获取社区支持

### 如何参与社区？

- 加入微信技术交流群分享项目和交流经验
- 在 GitHub 上 Star 项目并提交 Issue 或 PR
- 关注官方文档获取最新功能更新

