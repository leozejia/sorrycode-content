---
title: Plugins vs Skills - What's the Difference
slug: plugins-vs-skills
order: 1
summary: Plugins give agents new tools, while Skills teach agents how to work. They have different use cases, installation methods, and calling syntax.
section: runtime
section_title: Models & Runtimes
section_order: 10
group: general
group_title: General
group_order: 40
---

# Plugins vs Skills - What's the Difference

If you see both Plugins and Skills in Codex or Claude Code, you might wonder how they relate.

**Short answer:**

- **Plugins** give agents **new tools** (like browser control, desktop operations)
- **Skills** teach agents **how to work** (like generating images, formatting documents)
- **They're not mutually exclusive** - some capabilities can exist as both Plugin and Skill

<h2 id="quick-comparison">Quick Comparison</h2>

| Dimension | Plugins | Skills |
|-----------|---------|--------|
| **Nature** | System-level tool extension | Workflow knowledge package |
| **Provides** | New capabilities (like browser control) | Work methods (like image generation flow) |
| **Invocation** | `@PluginName` (e.g. `@Chrome`) | Natural language (e.g. "use Kami...") |
| **Installation** | Visual UI or config file | `npx skills install` or ask agent |
| **Scope** | Codex App, Claude Code (CLI & Desktop) | Works on both Codex and Claude Code |

<h2 id="what-are-plugins">What Are Plugins</h2>

Plugins give agents new tools.

**Common Plugins:**

- **@Chrome** - Operate real Chrome browser (for sites requiring login)
- **@Computer** - Operate desktop system (system settings, permission checks)
- **@Browser** - Test local web pages (localhost debugging)
- **Spreadsheets** - Create and edit spreadsheets
- **Presentations** - Create and edit presentations
- **Documents** - Create and edit documents

**Invocation examples:**

```text
@Chrome open X and read this post for me
@Computer open System Settings and check screen recording permissions
@Browser open http://localhost:3000 and test the login flow
```

<h2 id="what-are-skills">What Are Skills</h2>

Skills teach agents how to work.

**Common Skills:**

- **SorryCode Image2** - Image generation workflow and standards
- **Kami** - One-pager layout methods
- **Office Docs** - Word, Excel, PowerPoint workflows
- **Waza** - Code review steps
- **Ponytail** - Design workflow (also exists as Plugin)

**Invocation examples:**

```text
Use SorryCode Image2 to generate a cover image
Use Kami to format this content into a one-pager
Use Waza to check this change
```

<h2 id="key-difference">Key Difference</h2>

### Plugins: Provide Tools

Plugins give agents **new capabilities**, like installing a mechanical arm or adding radar to a car.

**Example:**
- Without Chrome Plugin: agent cannot operate real browser
- With Chrome Plugin: agent can control your Chrome and operate logged-in sites

### Skills: Provide Methods

Skills teach agents **how to use tools**, like teaching humans to drive or cook.

**Example:**
- Without Kami Skill: agent doesn't know how to layout a one-pager
- With Kami Skill: agent knows one-pager layout rules, font choices, information hierarchy

### They Can Coexist

Some capabilities can exist as both Plugin and Skill:

**Example - Ponytail:**
- **Ponytail Plugin**: Provides underlying design tool capabilities
- **Ponytail Skill**: Teaches agent how to use these tools for design tasks

<h2 id="installation">How to Install</h2>

### Install Plugins in Codex App

**Method 1: Visual Interface (Recommended)**

1. Open Codex App
2. Click "Plugins" in the sidebar
3. Browse Featured, Productivity, and other categories
4. Click "Try in chat" or install button next to plugins
5. Installed plugins appear in the "Installed" section

**Method 2: Config File (Fallback)**

If visual interface is unavailable, manually edit:

```text
~/.codex/config.toml
```

Add:

```toml
[plugins."chrome@openai-bundled"]
enabled = true

[plugins."computer-use@openai-bundled"]
enabled = true
```

Save and restart Codex App.

**Additional dependencies:**
- Chrome Plugin requires [Codex Chrome Extension](https://chromewebstore.google.com/detail/codex/hehggadaopoacecdllhhajmbjkdcmajg)
- Computer Use requires granting macOS screen recording and accessibility permissions

### Install Plugins in Claude Code Desktop (Beta)

**Note: This feature is currently in Beta.**

1. Open Claude Code Desktop
2. Go to Settings > Plugins & skills
3. In the "PLUGIN MARKETPLACES" section
4. Add Git repository as plugin source
5. Plugins install to `/Library/Application Support/Claude/org-plugins`

### Install Skills

**Command line installation:**

```bash
npx skills install <skill-name>
```

**Ask agent to install:**

```text
Please install the SorryCode Image2 skill for me
```

**Uninstall:**

```bash
npx skills remove --global <skill-name>
```

<h2 id="compatibility">Compatibility</h2>

| Runtime | Plugins | Skills |
|---------|---------|--------|
| Codex App | ✅ Full support | ✅ Full support |
| Codex CLI | ⚠️ Partial support | ✅ Full support |
| Claude Code CLI | ✅ Full support | ✅ Full support |
| Claude Code Desktop | 🧪 Beta support | ✅ Full support |
| Claude Desktop | ❌ Not supported | ❌ Not supported |

**Notes:**

- Plugins work best in Codex App and Claude Code CLI
- Claude Code Desktop's Plugin support is experimental
- Skills are based on open agent skills standard, work across runtimes
- Claude Desktop only supports third-party inference gateway, not Plugins or Skills

**Using Plugins in Claude Code CLI:**

```bash
# View available plugin commands
/plugin

# Manage Claude Code plugins
/plugin (plugins)

# Activate pending plugin changes
/reload-plugins
```

<h2 id="when-to-use">When to Use Which</h2>

### Use Plugins When

- Need to operate real browser (not headless)
- Need access to logged-in websites (X, GitHub, Gmail)
- Need to operate desktop apps or system settings
- Need specific system-level capabilities

### Use Skills When

- Need reusable workflows (design, documents, code review)
- Need cross-runtime use (works on both Codex and Claude Code)
- Want team to follow unified standards
- Repeatedly do same type of task, want agent to remember method

### Use Both Together

They don't conflict and can combine:

```text
Example workflow:
1. Use @Chrome to log into Figma, export design assets
2. Use SorryCode Image2 Skill to generate brand-consistent images
3. Use Office Docs Skill to format content into document
4. Use @Browser to preview final result
```

<h2 id="technical-difference">Technical Differences</h2>

### Plugins

- **Install location**: System-level (Codex App) or organization-level (Claude Code Desktop)
- **Launch timing**: Globally enabled, loaded at runtime startup
- **Permission needs**: May require system permissions (screen recording, accessibility, browser extension)
- **Invocation syntax**: `@PluginName`
- **Nature**: System-level capability extension

### Skills

- **Install location**: `~/.agents/skills/` or project `.agents/skills/`
- **Structure**: `SKILL.md`, `description`, `references/`, `scripts/`, `assets/`
- **Loading mechanism**: Progressive disclosure (reads description first, loads full content when needed)
- **Invocation syntax**: Natural language or explicit naming
- **Nature**: Workflow knowledge package

<h2 id="why-both">Why Two Mechanisms</h2>

**Plugins: Capability Boundary**

Some things agents can't do not because they don't know how, but because they **physically lack the capability**.

Examples:
- Agent cannot operate your Chrome (unless Chrome Plugin installed)
- Agent cannot control desktop (unless Computer Use Plugin installed)

**Skills: Knowledge Boundary**

Some things agents can do but **don't know your workflow and standards**.

Examples:
- Agent can generate images but doesn't know your brand guidelines
- Agent can write code but doesn't know your review standards

**They solve different problems:**

| Problem Type | Solution |
|-------------|----------|
| Agent can't do it | Install Plugin for new capability |
| Agent doesn't know how | Install Skill for workflow |
| Agent can do it but inconsistently | Install Skill for unified standards |

<h2 id="with-mcp">How Plugins, Skills, and MCP Relate</h2>

Three different positions that can combine:

- **Plugins** - System-level tools (browser, desktop, specialized services)
- **Skills** - Workflow knowledge (how to complete tasks)
- **MCP** - Data connection protocol (read databases, call APIs)

**Combination example:**

```text
Complete workflow:
1. Read customer data from database via MCP
2. Use @Chrome Plugin to log into CRM system
3. Use DBSkill to analyze data and generate report
4. Use Office Docs Skill to format into document
```

<h2 id="common-questions">Common Questions</h2>

### Can I use Plugins after API login in Codex App?

**Yes.** Plugins are local capability extensions, not dependent on Codex official accounts.

### Why do some capabilities exist as both Plugin and Skill?

Because they solve problems at different layers:
- **Plugin layer**: Provides underlying capabilities
- **Skill layer**: Provides workflow guidance

### Is Claude Code Desktop's Plugins feature stable?

**Currently Beta status.** Recommendations:
- Production environments prioritize Skills
- Experimental work can try Plugins (Beta)

### How do I know if I need Plugin or Skill?

Ask yourself:
- Can agent do it? → No → Need Plugin
- Does agent know how? → No → Need Skill
- Does agent do it consistently? → No → Need Skill

<h2 id="next">What's Next</h2>

**If you want to install Plugins:**

- Codex App users: Open "Plugins" in sidebar, browse and install visually
- Claude Code CLI users: Use `/plugin` command to manage plugins
- Claude Code Desktop users: Settings > Plugins & skills (Beta feature)

**If you want to install Skills:**

- See [Skills / Featured Skills](/docs/skills/featured-skills) to find suitable skills
- Or see [Make AI Remember Work Methods](/docs/agent-memory/remember-skills) to learn how to create your own
