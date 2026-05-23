# draft-goal-skill 中文文档

[English](README.md) | [skills.sh 项目页](https://www.skills.sh/juzhengsi/draft-goal-skill) | [draft-goal 技能页](https://www.skills.sh/juzhengsi/draft-goal-skill/draft-goal)

`draft-goal-skill` 是一个面向 AI Agent 的目标定稿技能。它可以把模糊、过大的自然语言需求，转换成可审阅、可验证、可迭代的 `/goal` 目标说明。

这个技能的重点不是立刻生成最终 goal，而是先判断是否真的需要 goal，再通过必要的澄清问题和用户充分交流，先输出草稿，最后在用户确认后再定稿。

## 文档入口

- [技能源码：SKILL.md](skills/draft-goal/SKILL.md)
- [OpenAI/Agent 界面配置](skills/draft-goal/agents/openai.yaml)
- [适合使用 goal 的示例](examples/suitable-goal.md)
- [不适合使用 goal 的示例](examples/not-suitable.md)
- [需要继续澄清的示例](examples/needs-clarification.md)
- [skills.sh 自定义展示配置](skills.sh.json)

## 它能做什么

- 判断当前需求是否适合使用 `/goal`。
- 如果需求很简单，不强行生成 goal，而是给出更清晰的普通 prompt 建议。
- 把复杂需求拆成六个关键字段：
  - 目标结果
  - 验证证据
  - 约束条件
  - 执行边界
  - 迭代策略
  - 阻塞停止条件
- 在信息不足时，先提出少量关键澄清问题。
- 先输出可审阅的草稿，而不是直接定稿。
- 只有在用户确认后，才输出最终 `/goal`。

## 适合什么时候用

适合路径不确定、需要反复尝试、需要明确验收证据的任务，例如：

- 持续修复一个不稳定测试，直到修复或明确阻塞。
- 迁移复杂依赖，同时确保行为不回退。
- 通过多轮实验提升某个 benchmark 指标。
- 复现或审计一篇研究结果。
- 把一个模糊项目需求整理成可执行、可验证的目标合同。

## 不适合什么时候用

下面这些简单任务不需要 `/goal`：

- 修改一个 CSS 规则。
- 运行一个命令。
- 解释一条报错信息。
- 对一个已知文件做直接编辑。

遇到这类情况时，这个 skill 应该说明“当前需求没有必要使用 goal”，并给出一个更清晰的普通 prompt，而不是强行创建 goal。

## 安装

从 GitHub 安装：

```bash
npx skills add JuzhengSi/draft-goal-skill
```

从本地仓库安装：

```bash
npx skills add .
```

手动复制到 Agent 的 skills 目录：

```bash
cp -R skills/draft-goal .agents/skills/draft-goal
```

如果你的 Agent 使用不同的 skills 目录，请把目标路径替换成对应位置。

## 使用方式

通过技能名调用：

```text
$draft-goal 我希望 agent 持续修复这个 flaky checkout test，直到它被修好并有测试证据，或者明确说明为什么被阻塞。
```

如果任务适合 goal，技能通常会先列出已知信息和待确认问题。用户补充关键回答后，它会输出草稿。用户确认后，才输出最终可复制的 `/goal`。

如果任务不适合 goal，技能会直接说明原因，并给出一个更适合作为普通请求的 prompt。

## 推荐工作流

1. 先判断是否需要 goal。
2. 如果信息不足，提出不超过三个关键问题。
3. 输出草稿，并明确标注假设。
4. 等用户确认或修改。
5. 确认后再输出最终 `/goal`。

## 项目结构

```text
README.md
README.zh.md
LICENSE
skills.sh.json
examples/
skills/draft-goal/SKILL.md
skills/draft-goal/agents/openai.yaml
```

这个结构符合 skills.sh 推荐的仓库布局：实际技能文件位于 `skills/draft-goal/SKILL.md`，因此 skills.sh 可以为它生成独立技能页面。

## 许可证

MIT
