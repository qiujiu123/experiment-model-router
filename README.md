# experiment-model-router

<!-- [Codex] 公开发布版 1.1.1，2026-10-14。 -->

面向科研实验迭代的 Codex 技能：由 **GPT-6.1 Sol / MAX** 编码与运行实验，再由 **GPT-6 Astra / 极高** 分析证据并设计下一步。

## 工作流程

已有方案 → Sol 编码、运行、保存原始结果 → 确认实验成功、失败或中止 → Astra 分析与设计 → 在用户已授权的轮数和预算内继续。

需要先设计方案时从 Astra 开始；只要求分析时不启动训练。两个阶段串行交接，通过项目内 Markdown 记录、代码、日志和原始结果共享证据。

## 安装

将本仓库完整克隆到 Codex 的个人技能目录，目录名保持 `experiment-model-router`。例如 Windows PowerShell：

```powershell
git clone https://github.com/qiujiu123/experiment-model-router.git "$env:USERPROFILE/.codex/skills/experiment-model-router"
```

若配置了其他技能目录（例如自定义 CODEX_HOME），使用对应位置。目标目录已存在时先检查现有修改，不直接覆盖。技能未显示时重新打开聊天或重启应用。

## 使用

```text
使用 $experiment-model-router，按当前方案运行本轮实验，完成后分析结果并设计下一步。
```

允许自动匹配实验类任务；自动触发并实际执行后，最终结果末尾会说明本次使用了该技能。自动匹配不是强制系统钩子。连续多轮执行应给出目标、轮数或资源预算。

## 所需能力与边界

- 运行平台必须提供可指定模型和推理强度的子代理工具，并允许访问上述两个模型。
- 对当前 Codex 协作接口，Sol 请求 `reasoning_effort="max"`，Astra 请求 `reasoning_effort="xhigh"`，均使用 `fork_turns="none"`。
- 技能调度的是子代理；不会切换主聊天界面模型，也不是后台训练调度服务。
- 工具缺失或模型不可用时明确报告，不用提示词模拟“换模型”。
- 模型和推理强度请求被工具接受，不等于服务端实际设置已独立核验。

## 验证情况

本地完成过 Sol MAX → Astra 极高的隔离线性回归测试：程序退出码为0，数值校验和原始证据交接通过。此结果不代表真实长时训练、所有平台或无上下文新聊天的自动触发已经验证。

公开版本保留默认路由与实验记录规则，移除了个人绝对路径和专用依赖镜像。本仓库提供技能说明和界面元数据，不附带模型权重、API凭据、训练数据或实验产物。

## 文件

- [SKILL.md](SKILL.md)：实际技能入口。
- [agents/openai.yaml](agents/openai.yaml)：显示信息和自动匹配设置。
- [CHANGELOG.md](CHANGELOG.md)：版本与修改记录。

采用 [MIT License](LICENSE)。
