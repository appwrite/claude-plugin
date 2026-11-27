# Appwrite Claude Code Plugin

![License](https://img.shields.io/badge/license-BSD--3--Clause-blue.svg?style=flat-square)
![Version](https://img.shields.io/badge/version-0.4.0-blue.svg?style=flat-square)
[![X Account](https://img.shields.io/badge/follow-%40appwrite-000000?logo=x&style=flat-square)](https://x.com/appwrite)
[![Discord](https://img.shields.io/discord/564160730845151244?label=discord&style=flat-square)](https://appwrite.io/discord)

Appwrite tools for Claude Code. This plugin packages Appwrite SDK skills, the hosted Appwrite MCP server, and deployment commands in Claude Code's native plugin format.

## Installation

The plugin is listed in Anthropic's official marketplace, which Claude Code adds automatically. Install it from your shell:

```sh
claude plugin install appwrite@claude-plugins-official
```

Or from a Claude Code session:

```text
/plugin install appwrite@claude-plugins-official
```

To install from this repository instead, add it as a marketplace first:

```text
/plugin marketplace add appwrite/claude-plugin
/plugin install appwrite@appwrite
```

Run `/reload-plugins` to load the plugin in a session that is already open.

## Included skills

- `/appwrite:typescript`
- `/appwrite:dart`
- `/appwrite:kotlin`
- `/appwrite:swift`
- `/appwrite:php`
- `/appwrite:python`
- `/appwrite:ruby`
- `/appwrite:go`
- `/appwrite:rust`
- `/appwrite:dotnet`
- `/appwrite:cli`

These skills give Claude Code language-specific Appwrite context for authentication, database queries, storage, realtime, functions, and server-side administration. Claude loads them automatically when a task matches, or you can invoke one directly.

## Code review skills

These skills work with Appwrite Review, which reviews GitHub pull requests and grades them from **S** to **F**.

| Skill | What it does |
| --- | --- |
| `/appwrite:review-status` | Read the current tier, open findings, and filtered-out comments. Does not start a review. |
| `/appwrite:review-loop` | Fix the pull request until Appwrite Review grades it **Tier S** and no comments are left open. |
| `/appwrite:review-learn` | Reply on a finding with a lasting rule so Appwrite Review remembers it. |
| `/appwrite:review-setup` | Write `.hansi.json` and open a pull request onto the base branch. |

`review-threads` is not invoked directly: it keeps Claude from resolving review threads that Appwrite Review clears itself after a fix or a dismissal.

The review skills need Appwrite Review set up on the repository (Console → your project → Review) and a way to talk to GitHub; the examples use the GitHub CLI. Each review counts toward the project's review usage, and `review-loop` stops after 5 iterations.

## Included commands

- `/appwrite:deploy-site`
- `/appwrite:deploy-function`

These commands are manual-only, so Claude does not start a deployment on its own.

## Hosted MCP server

The plugin configures one `appwrite` server at `https://mcp.appwrite.io/`. It provides tools for working with your Appwrite organizations and projects, and for searching the latest Appwrite documentation.

The hosted server uses browser-based OAuth, so the plugin does not require an API key, project ID, endpoint, or other manually configured secret. In a Claude Code session, open `/mcp`, select the `appwrite` server, and choose **Authenticate**. From your shell, run:

```sh
claude mcp login plugin:appwrite:appwrite
```

After authentication, try:

> Use Appwrite to show my workspace context and list my projects.

If authentication expires, choose **Re-authenticate** from `/mcp` or run the login command again. If the browser does not open, use the URL printed by Claude Code. Run `claude mcp get plugin:appwrite:appwrite` to check the server's authentication and connection status.

## Structure

```text
.claude-plugin/
├── plugin.json              # Plugin manifest
└── marketplace.json         # Marketplace manifest
skills/                      # Claude Code skills (per language)
├── typescript/
│   └── SKILL.md
├── dart/
│   └── SKILL.md
├── kotlin/
│   └── SKILL.md
├── swift/
│   └── SKILL.md
├── php/
│   └── SKILL.md
├── python/
│   └── SKILL.md
├── ruby/
│   └── SKILL.md
├── go/
│   └── SKILL.md
├── rust/
│   └── SKILL.md
├── dotnet/
│   └── SKILL.md
├── cli/
│   └── SKILL.md
├── review-status/            # Code review skills
│   └── SKILL.md
├── review-loop/
│   └── SKILL.md
├── review-learn/
│   └── SKILL.md
├── review-setup/
│   └── SKILL.md
└── review-threads/
    └── SKILL.md
commands/                    # Manual commands with side effects
├── deploy-site.md
└── deploy-function.md
.mcp.json                    # Hosted Appwrite MCP server
```

## Local development

From a clone of this repository, validate the plugin and marketplace:

```sh
claude plugin validate .
```

Load the plugin directly for a development session:

```sh
claude --plugin-dir .
```

Then check that `/help` lists the `appwrite` namespace and that `/appwrite:typescript` loads the TypeScript skill.

To test the install-by-name flow, add the clone as a local marketplace:

```sh
claude plugin marketplace add ./ --scope local
claude plugin install appwrite@appwrite --scope local
```

## Learn more

- [Appwrite in Claude Code](https://appwrite.io/docs/tooling/ai/agents/claude-code)
- [Appwrite MCP server](https://appwrite.io/docs/tooling/ai/mcp-servers)
- [Claude Code plugins documentation](https://code.claude.com/docs/en/discover-plugins)

## Contribution

This library is auto-generated by Appwrite custom [SDK Generator](https://github.com/appwrite/sdk-generator). To learn more about how you can help us improve this SDK, please check the [contribution guide](https://github.com/appwrite/sdk-generator/blob/main/CONTRIBUTING.md) before sending a pull-request.

## License

Please see the [BSD-3-Clause license](https://raw.githubusercontent.com/appwrite/appwrite/master/LICENSE) file for more information.
