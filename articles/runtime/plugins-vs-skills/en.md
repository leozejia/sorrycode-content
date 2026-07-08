---
title: Plugins vs Skills - What's the Difference
slug: plugins-vs-skills
order: 4
summary: Plugins give agents new tools, Skills teach agents how to work—completely different use cases, installation methods, and calling syntax.
section: runtime
section_title: Runtime
section_order: 10
---

# Plugins vs Skills - What's the Difference

If you see both Plugins and Skills in Codex or Claude Code, you might wonder if they are the same thing.

**Short answer:**

- **Plugins** extend what tools an agent can use, such as operating browsers, controlling desktops, or making videos
- **Skills** teach an agent how to handle specific tasks, such as generating images, formatting documents, or reviewing code

One extends capability boundaries, the other teaches work methods.

<h2 id="quick-comparison">Quick Comparison</h2>

| Dimension | Plugins | Skills |
|-----------|---------|--------|
| **Nature** | System-level capability extension | Workflow operation manual |
| **Scope** | Mainly Codex App | Works on both Codex and Claude Code |
| **Invocation** | `@Chrome`, `@Computer` | Natural language, like "use Kami..." |
| **Installation** | Edit config file + restart | `npx skills install` |
| **Typical use** | Operate browser, desktop, specialized services | Content creation, document handling, code review |

<h2 id="what-are-plugins">What Are Plugins</h2>

Plugins are Codex-specific external capability extensions. They let agents operate browsers, control desktops, or connect to specialized services.

**Common Plugins:**

- **@Chrome** - Operate real Chrome browser, suitable for sites requiring login state (X, GitHub, Gmail, Stripe)
- **@Browser** - Test local web pages, suitable for localhost debugging, screenshots, form flow validation
- **@Computer** - Operate desktop system, suitable for system settings, permission checks, desktop apps
- **@HyperFrames** - Create HTML videos and motion graphics

**Invocation examples:**

```text
@Chrome open X and read this post for me
@Browser open http://localhost:3000 and test the login flow
@Computer open System Settings and check screen recording permissions
@HyperFrames make a 10-second product intro video
```

**Technical characteristics:**

- Configured in `~/.codex/config.toml` and requires Codex App restart
- Chrome requires installing extension and native host
- Computer Use requires granting macOS screen recording and accessibility permissions
- Globally enabled, loaded at runtime startup

<h2 id="what-are-skills">What Are Skills</h2>

Skills are installable, reusable workflow capability packages. They teach agents how to handle specific types of tasks without changing the agent's basic toolset.

**Common Skills:**

- **SorryCode Image2** - Generate images, design covers, create illustrations
- **Kami** - Format content into one-pagers
- **Office Docs** - Edit Word, Excel, PowerPoint
- **Waza** - Code review, pre-commit checks
- **DBSkill** - Business diagnostics, competitive analysis

**Invocation examples:**

```text
Use SorryCode Image2 to generate a cover image
Use Kami to format this content into a one-pager
Use Waza to check this change
```

**Technical characteristics:**

- Based on open agent skills standard, works on both Codex and Claude Code
- Installed via `npx skills install` to `~/.agents/skills` or project `.agents/skills`
- Progressive disclosure: agent reads description first, loads full SKILL.md only when needed
- May include scripts, templates, fonts, sample files

<h2 id="when-to-use">When to Use Which</h2>

### Use Plugins When

- You need to operate a real browser, not a headless one
- You need access to logged-in websites (X, GitHub, Gmail, Stripe, Google Cloud Console)
- You need to operate desktop apps or system settings
- You need multi-tab coordination, screenshots, form automation
- You need to create HTML videos or motion graphics

### Use Skills When

- You need reusable business workflows (design, documents, code review)
- You need cross-runtime capabilities (works on both Codex and Claude Code)
- Team collaboration requires unified work standards
- You repeatedly ask agents to do the same type of thing and want them to remember the method
- You need to teach domain knowledge or operational standards

<h2 id="installation">Installation Comparison</h2>

### Installing Plugins

Plugins are mainly configured in Codex App.

Edit the config file:

```text
~/.codex/config.toml
```

Add this block:

```toml
[plugins."browser-use@openai-bundled"]
enabled = true

[plugins."chrome@openai-bundled"]
enabled = true

[plugins."computer-use@openai-bundled"]
enabled = true

[plugins."hyperframes@openai-curated"]
enabled = true
```

Save, fully quit, and restart Codex App.

**Additional dependencies:**

- Chrome requires [Codex Chrome Extension](https://chromewebstore.google.com/detail/codex/hehggadaopoacecdllhhajmbjkdcmajg) and native host
- Computer Use requires granting macOS screen recording and accessibility permissions

### Installing Skills

Skills can be installed via command line or by asking the agent to read documentation and install.

**Command line installation:**

```bash
npx skills install <skill-name>
```

**Ask agent to install:**

```text
Please install the SorryCode Image2 skill for me
```

The agent will automatically detect the current environment, check dependencies, and execute installation.

After installation, restart Codex or Claude Code to use.

**Uninstall:**

```bash
npx skills remove --global <skill-name>
```

<h2 id="compatibility">Compatibility</h2>

| Runtime | Plugins | Skills |
|---------|---------|--------|
| Codex App | ✅ Supported | ✅ Supported |
| Codex CLI | ⚠️ Partial support | ✅ Supported |
| Claude Code CLI | ❌ Not supported | ✅ Supported |
| Claude Code Desktop | ❌ Not supported | ✅ Supported |
| Claude Desktop | ❌ Not supported | ❌ Not supported |

**Notes:**

- Plugins are Codex ecosystem exclusive, mainly used in Codex App
- Skills are based on open standards, work across runtimes
- Claude Desktop only supports third-party inference gateway, does not support Plugins or Skills

<h2 id="technical-difference">Technical Differences</h2>

### Plugins

- Configured in `~/.codex/config.toml`
- Globally enabled, loaded at runtime startup
- Requires additional permissions (browser extension permissions, system permissions)
- Invocation syntax is `@PluginName`
- Essentially system-level capability extensions

### Skills

- Installed to `~/.agents/skills/` or `.agents/skills/`
- Structure includes `SKILL.md`, `description`, `references/`, `scripts/`, `assets/`
- Progressive disclosure: agent reads description first to determine need, loads full content only when required
- Invocation syntax is natural language
- Essentially workflow operation manuals

<h2 id="api-login">Can Codex App Use Plugins After API Login?</h2>

**Yes.**

Now Codex App can use Plugins normally after API login (such as connecting to SorryCode Gateway).

Configuration is the same as with account login:

1. Edit `~/.codex/config.toml`
2. Add Plugins configuration
3. Restart Codex App

Plugins are local capability extensions and do not depend on Codex official accounts. As long as Codex App runs normally, Plugins work.

<h2 id="can-they-work-together">Can Plugins and Skills Work Together?</h2>

**Yes.**

They do not conflict.

For example, you can:

1. Use `@Chrome` to log into Salesforce and fetch customer data
2. Use DBSkill to analyze this data and generate diagnostic reports
3. Use Office Docs skill to format the report into a Word document
4. Use SorryCode Image2 to generate the report cover

Plugins extend capability boundaries, Skills teach work methods. Combining both can complete more complex workflows.

<h2 id="with-mcp">How Do Plugins, Skills, and MCP Relate?</h2>

The three have different positions:

- **MCP (Model Context Protocol)** - Tool and data connection protocol, lets agents read databases, call APIs, access external systems
- **Plugins** - Codex-specific system capability extensions, give agents browsers, desktops, specialized services
- **Skills** - Workflow capability packages, teach agents how to handle specific types of tasks

They can combine:

- An image skill can call an image API connected via MCP
- A data analysis skill can read databases via MCP, then use `@Browser` to display visualization results
- A testing skill can use `@Chrome` to operate a real browser, then record test results via MCP

<h2 id="next">Next Steps</h2>

**If you want to use Plugins:**

- Codex App users can directly configure `~/.codex/config.toml`
- Claude Code users do not currently support Plugins, consider using Skills or MCP

**If you want to use Skills:**

- First read [Agent Infra / Skills](/docs/agent-memory/remember-skills) to understand Skills standards
- Then read [Skills / Featured Skills](/docs/skills/featured-skills) to find skills that suit you
- Or directly ask the agent to read the current Skills list and recommend based on your goals

**If you are unsure:**

Ask the agent:

```text
I want you to operate Gmail, should I use a Plugin or a Skill?
I want you to always follow brand guidelines when generating images, should I use a Plugin or a Skill?
```

The agent will give recommendations based on task characteristics.
