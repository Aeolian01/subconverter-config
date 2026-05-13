# subconverter-config

基于 ACL4SSR / subconverter 外部配置改造的 Mihomo 订阅转换配置仓库。

## 目标
- 将 AI 流量拆分为 **OpenAI / Gemini / Anthropic** 三个独立分组
- 使用 Clash 文本规则源，避免把 sing-box 二进制规则集直接交给 `ini` 模板解析
- 提供港 / 美落地节点分组和手动选择入口，兼容新版 Mihomo / Clash Verge Rev

## 文件
- `configs/ACL4SSR_Online_AI_Chain.ini`：推荐用于订阅转换后端的配置文件
- `Clash/config/ACL4SSR_Online_AI_Chain.ini`：同内容兼容路径
- `index.html`：静态配置生成器，可生成并发布同结构的 `ini`，并生成 Clash Verge Rev Script 覆写脚本

## 规则源
- OpenAI: `https://raw.githubusercontent.com/blackmatrix7/ios_rule_script/master/rule/Clash/OpenAI/OpenAI.list`
- Gemini: `https://raw.githubusercontent.com/blackmatrix7/ios_rule_script/master/rule/Clash/Gemini/Gemini.list`
- Anthropic: `https://raw.githubusercontent.com/blackmatrix7/ios_rule_script/master/rule/Clash/Claude/Claude.list`


客户端更新订阅后，可在 `🤖 OpenAi / 🤖 Gemini / 🤖 Anthropic` 中选择：

```text
🇭🇰 香港节点
🇺🇲 美国节点
☑️ 手动选择
DIRECT
```

## 关于链式代理
新版 Mihomo 已移除 `relay` 策略组，Clash Verge Rev 会报类似错误：

```text
unsupported type: The group [...] with relay type was removed, please using dialer-proxy instead
```

`dialer-proxy` 需要写在具体代理节点或 proxy-provider override 上；subconverter 的普通 `ini` 外部配置只负责 ruleset 和 proxy-group，不能可靠地给订阅中的每个节点批量追加 `dialer-proxy`。

因此本仓库默认配置已移除 `relay`，以保证订阅更新和配置检查通过。若必须实现真链式代理，需要在客户端侧使用 Mihomo 覆写/脚本，或维护支持 `proxy-providers.override.dialer-proxy` 的完整 YAML 配置。

GitHub Pages 中的生成器可自动生成 Clash Verge Rev 的 Script 覆写脚本。将脚本粘贴到 Clash Verge Rev 的 Script 增强配置并启用后，可通过 `dialer-proxy` 创建港 / 美落地链路节点。
