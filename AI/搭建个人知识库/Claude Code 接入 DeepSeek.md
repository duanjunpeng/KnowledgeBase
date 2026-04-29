
## 基础配置
1. 在用户目录下的 `~./claude` 文件夹中，新建 `settings.json` 配置文件：
```json ~/.claude/settings.json
{
	"env": {
		"ANTHROPIC_AUTH_TOKEN": "sk-你的 api key",
		"ANTHROPIC_BASE_URL": "https://api.deepseek.com/anthropic",
		"ANTHROPIC_MODEL": "deepseek-v4-pro", "ANTHROPIC_DEFAULT_OPUS_MODEL": "deepseek-v4-pro",
		"ANTHROPIC_DEFAULT_SONNET_MODEL": "deepseek-v4-pro",
		"ANTHROPIC_DEFAULT_HAIKU_MODEL": "deepseek-v4-pro",
		"CLAUDE_CODE_SUBAGENT_MODEL": "deepseek-v4-pro",
		"CLAUDE_CODE_MAX_OUTPUT_TOKENS": "32000"
	},
	"permissions": {
		"allow": [],
		"deny": []
	},
	"alwaysThinkingEnabled": false
}
```

## 配置参数详解

|参数|说明|备注|
|---|---|---|
|ANTHROPIC_AUTH_TOKEN|DeepSeek API 密钥|用于身份认证，请妥善保管|
|ANTHROPIC_BASE_URL|API 接口地址|核心配置！DeepSeek 提供的 Anthropic 兼容接口|
|ANTHROPIC_MODEL|默认模型|指定使用的 DeepSeek 模型|
|ANTHROPIC_DEFAULT_OPUS_MODEL|最复杂任务模型|适用于架构设计等高难度任务|
|ANTHROPIC_DEFAULT_SONNET_MODEL|日常编码模型|平衡性能与成本|
|ANTHROPIC_DEFAULT_HAIKU_MODEL|简单任务模型|快速响应，成本更低|
|CLAUDE_CODE_SUBAGENT_MODEL|子代理模型|自动化子任务使用的模型|
|CLAUDE_CODE_MAX_OUTPUT_TOKENS|最大输出长度|可根据需求调整，最高支持 32K|


## 为什么可以这样配置？

DeepSeek 提供了与 Anthropic API 格式完全兼容的接口。这意味着：
1. **协议兼容**：DeepSeek 的 API 响应格式与 Anthropic 一致
2. **无缝切换**：只需修改 `BASE_URL` 和认证 Token，无需修改任何代码
3. **功能完整**：支持流式输出、函数调用等核心特性