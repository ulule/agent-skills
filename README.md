# Ulule Agent Skills

Official Ulule Agent Skills for compatible AI assistants and agents. These skills map **crowdfunding, campaign, fundraising, presale, proposal, draft, rewards, goal and fundraising page** — and the French intents **collecte, campagne, financement participatif, prévente, brouillon, proposition, contreparties, objectif et page de collecte Ulule** — to two actions:

- submitting a project proposal to Ulule;
- creating and completing an unpublished project draft.

Both actions are available through the **MCP Public Ulule**.

```text
Endpoint   https://api.ulule.com/mcp/public
ID         com.ulule/mcp-public
Docs       https://developers.ulule.com/docs/mcp/
```

> The campaign is never published automatically.

## Available skills

### `ulule-crowdfunding`

Use this skill when a user wants to create, prepare, edit or recover an Ulule
crowdfunding campaign, fundraising project or presale. The user does not need to
mention MCP or an AI assistant.

The skill helps an assistant to:

- recognize crowdfunding, fundraising and presale intents;
- diagnose the project and request evidence instead of inventing facts;
- calculate a defensible goal from verified costs;
- prepare a clear page, honest visual brief, viable rewards and realistic plan;
- find and update an existing proposal instead of creating duplicates;
- distinguish a proposal, an unpublished project draft and a live campaign;
- connect to Ulule through the MCP Public Ulule when supported by the client.

## MCP Public Ulule

Endpoint:

```text
https://api.ulule.com/mcp/public
```

MCP Registry identifier:

```text
com.ulule/mcp-public
```

Documentation: <https://developers.ulule.com/docs/mcp/>

The server uses OAuth 2.1 with dynamic client registration and PKCE. Compatible
MCP clients handle authorization and the user approves access. Never paste an
access token into a conversation.

## Publication boundaries

The skill prepares proposals and unpublished drafts. It does not publish a
campaign automatically, guarantee approval or success, or replace Ulule's
moderation process. Ulule reviews the proposal while the user and their
assistant complete the draft: human approval of the proposal is not a
prerequisite for preparing the unpublished draft. The technical availability of
`project_id` may be asynchronous.

Always keep these stages separate:

1. Project proposal.
2. Unpublished project draft.
3. Live campaign.

The creator remains responsible for reviewing and completing the project and
following Ulule's submission flow. The campaign is never published automatically.

## Install as a Claude Code plugin

Add this repository as a marketplace, then install the plugin:

```bash
claude plugin marketplace add ulule/agent-skills
claude plugin install ulule-crowdfunding@ulule-agent-skills
```

The plugin bundles the `ulule-crowdfunding` skill and declares the MCP Public
Ulule (`https://api.ulule.com/mcp/public`). On first use, Claude starts the
Ulule OAuth flow; the user signs in and approves access. No token or secret is
stored in this repository. The campaign is never published automatically.

Other clients supporting the Agent Skills format can install the skill directly:

```bash
npx skills add ulule/agent-skills --skill ulule-crowdfunding
```

## Repository structure

```text
.claude-plugin/
├── plugin.json
└── marketplace.json
.mcp.json
skills/
└── ulule-crowdfunding/
    ├── SKILL.md
    └── references/
        ├── campaign-quality.md
        ├── mcp-connection.md
        ├── project-lifecycle.md
        └── publishing-boundaries.md
```

## License

Apache-2.0. See [LICENSE](LICENSE).
