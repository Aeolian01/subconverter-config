# subconverter-config

基于 ACL4SSR 多国家模板改造的订阅转换配置仓库。

## 目标
- 将 AI 流量拆分为 **OpenAI / Gemini / Anthropic** 三个独立分组
- 保留常见直连 / 广告 / 微软 / 苹果 / Telegram / 媒体等规则
- 提供 **港 / 美 AI 落地链** 入口，便于手动选择前置节点后再走落地节点

## 文件
- `Clash/config/ACL4SSR_Online_AI_Chain.ini`：订阅转换配置文件
- `rules/OpenAI.list`：OpenAI / ChatGPT 规则
- `rules/Gemini.list`：Gemini / Google AI 规则
- `rules/Anthropic.list`：Anthropic / Claude 规则

## 说明
用户提供的以下规则源：
- OpenAI: `https://github.com/MetaCubeX/meta-rules-dat/raw/refs/heads/sing/geo/geosite/openai.srs`
- Gemini: `https://github.com/MetaCubeX/meta-rules-dat/raw/refs/heads/sing/geo/geosite/google-gemini.srs`
- Anthropic: `https://github.com/MetaCubeX/meta-rules-dat/raw/refs/heads/sing/geo/geosite/anthropic.srs`

它们属于 **sing-box `.srs` 规则集**，不适合直接塞进 ACL4SSR 这种 `ini` 订阅转换模板里。

因此本仓库为 `ini` 版本提供了 Clash/Mihomo 更通用的 `.list` 规则写法，便于直接用于订阅转换。

## 使用
将 `Clash/config/ACL4SSR_Online_AI_Chain.ini` 作为订阅转换配置文件使用即可。

若你的客户端对 `relay` 组嵌套分组支持不完整，可改为直接选择 `🇭🇰 香港节点 / 🇺🇲 美国节点 / ☑️ 手动切换`，或后续再补客户端侧链式脚本。