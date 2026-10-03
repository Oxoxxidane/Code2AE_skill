# Code2AE Skill

[English](#english) · [中文](#中文)

## English

Code2AE is an agent skill for rebuilding HTML, Remotion, Hyperframe, and other code-based animation projects as editable After Effects projects. It guides the agent through source inspection, observation of the original output, reconstruction, and verification inside AE.

### Installation

Download or clone this repository, then name the folder `code2ae`:

```sh
git clone https://github.com/Oxoxxidane/Code2AE_skill.git code2ae
```

Place that complete folder in your agent's user skill directory, such as `~/.codex/skills/code2ae/` for Codex or `~/.claude/skills/code2ae/` for Claude Code.

### Requirements and usage

Complete these steps before using the skill:

1. Visit [www.arbifx.com](https://www.arbifx.com), download the ArbiFX plugin, and follow its installation instructions to install it in After Effects.
2. Register an account at [www.arbifx.com](https://www.arbifx.com) and sign in.
3. Open your account dashboard on the website and create an API Key.
4. In AE, open the **Start** window for your ArbiFX effect instance, then click the **API** button in the upper-right corner.
5. Enter the **API Key** you just created, verify it, and save the configuration.

**Use this skill only after the API Key has been successfully verified and the configuration has been saved.**

Before using this skill in your agent, open AE and apply the **ArbiFX/AFX** effect to any layer at least once.

Ask your agent to use `code2ae` and provide the source project, for example:

> Use code2ae to rebuild this Remotion project as an editable After Effects project, faithfully reproduce its visuals and motion, and verify the result in AE.

## 中文

Code2AE 是一个指导 AI Agent 将 HTML、Remotion、Hyperframe 及其他代码动画工程重建为可编辑 After Effects 工程的 Skill。它要求先理解源代码并观察实际输出，再重建画面、运动与工程结构，最后在真实 AE 中检查和修正。

### 安装

下载或克隆本仓库后，将文件夹命名为 `code2ae`：

```sh
git clone https://github.com/Oxoxxidane/Code2AE_skill.git code2ae
```

把整个文件夹放入所用 Agent 的用户技能目录，例如：

| Agent | 用户技能目录 |
|---|---|
| Codex | `~/.codex/skills/code2ae/` |
| Claude Code | `~/.claude/skills/code2ae/` |

### 使用前提与开始方式

请先完成以下设置：

1. 前往 [www.arbifx.com](https://www.arbifx.com) 下载 ArbiFX 插件，并按安装说明安装到 After Effects。
2. 在 [www.arbifx.com](https://www.arbifx.com) 注册并登录账号。
3. 进入网站的用户后台，创建一个 API Key。
4. 打开 AE 中 ArbiFX 插件实例的 **Start** 窗口，点击窗口右上角的 **API** 按钮。
5. 填入刚创建的 **API Key**，进行验证并保存配置。

**确认 API Key 验证成功且配置已保存后，才可以使用本 Skill。**

在 Agent 中使用本 Skill 前，请先打开 AE，并在任意图层上应用一次 **ArbiFX/AFX** 效果。

在 Agent 中点名 `code2ae` 并提供源工程，例如：

> 使用 code2ae，将这个 Remotion 工程重建为可编辑的 AE 工程，忠实还原画面和动画，并完成实际 AE 检查。
