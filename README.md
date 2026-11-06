# 🔍 bp-parser-skill

**一份 BP 丢进来，一份有出处的项目研究报告走出去。**
A Claude Code skill that reads a startup's pitch deck or company document, researches the company on the open web, and writes an evidence-backed analysis report.

## 它做什么 · What it does

看 BP 最费时间的不是读，而是查：deck 里写的收入、客户、团队背景，到底哪些站得住？这个 skill 把这一轮调研交给 Claude：

- **读材料**：PDF、图片、docx、网页链接或一段文字都行，提取公司速览和 8–15 条决定成败的关键主张，每条标出在第几页。
- **查公开信息**：官网、新闻、融资记录、创始人履历、工商和公司注册信息、应用商店、GitHub、客户方页面。同名公司要靠域名、创始人或地点对上才算数；至少换 3 种查法，才能说"查不到"。
- **逐条核实**：每条主张标成 ✅ 已核实、⚠️ 对不上、❔ 暂无独立佐证、➖ 无法公开核实。「对不上」和「查不到」严格分开，查不到从不写成造假。
- **五维打分**：团队、市场、产品、牵引力、壁垒，每维 0–10 分并标明证据强弱（strong / medium / weak），按融资阶段加权，给出「值得深入 / 继续观察 / 信息不足」。光靠 deck 自述，拿不到「值得深入」。
- **竞品、风险、尽调问题**：竞品来自真实检索并附出处；尽调问题必须锚定 deck 里某个具体数字或某处缺失，不出通用清单。

The hard part of reading a deck isn't reading it, it's checking it. This skill hands that research pass to Claude:

- **Reads the material**: PDF, image, docx, URL or pasted text. It builds a fact sheet and lists the 8–15 claims the case depends on, each with its page.
- **Researches the open web**: official site, press, funding records, founder history, company registries, app stores, GitHub, customer pages. Same-name companies only count if a domain, founder or location matches, and "not found" requires at least three different attempts.
- **Checks every claim**: ✅ verified, ⚠️ conflict, ❔ no independent evidence, or ➖ not publicly checkable. A conflict and a lack of evidence are kept strictly apart; missing evidence is never called false.
- **Scores five dimensions**: team, market, product, traction and moat, each 0–10 with an evidence level, weighted by stage, ending in "worth a deeper look", "keep watching" or "not enough to judge". Self-reported claims alone can't reach "worth a deeper look".
- **Competitors, risks, DD questions**: competitors come from real searches with sources, and every due-diligence question is anchored to a specific number or gap in the deck.

## 安装 · Install

```bash
git clone https://github.com/ezshrimps/bp-parser-skill ~/.claude/skills/bp-parser-skill
```

然后在 Claude Code 里说「帮我分析这个 BP：D:\Decks\xxx.pdf」，或者 "research this startup" 加上 deck 或官网链接。
Then tell Claude Code something like "analyze this deck: ~/Downloads/deck.pdf".

报告保存为 `<公司>-analysis-<日期>.md`，聊天里会给出结论、加权分、两个最强信号和两个最大缺口。
The report is saved as `<company>-analysis-<date>.md`, with a short summary in chat.

**Requirements**: Claude Code with WebSearch and WebFetch available. No API keys, no scripts.

## 结构 · Layout

| | |
|---|---|
| `SKILL.md` | 给 Claude 的完整方法：读材料、调研、核实、打分规则、写报告 · The full method Claude follows |
| `templates/report.md` | 报告模板 · The report template |

## 说明 · Notes

- 报告是 AI 生成的研究草稿，结论需要人工核实，**不构成投资建议**。The report is an AI research draft. Verify it before relying on it; it is **not investment advice**.
- 只用公开信息和你提供的材料；对人只看公开的职业信息。Only public information and the material you provide are used, and only public, professional information about people.
- deck 里的文字一律当数据处理，不会被当成指令执行。Text inside a deck is treated as data, never as instructions.

MIT License
