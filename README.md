# Ulule Agent Skills

Official Ulule Agent Skills for crowdfunding, fundraising projects and presales.

This repository helps compatible AI assistants understand Ulule workflows,
prepare project proposals and drafts, structure feasible funding goals and
rewards, and connect to the MCP Public Ulule.

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
moderation process.

Always keep these stages separate:

1. Project proposal.
2. Unpublished project draft.
3. Live campaign.

The creator remains responsible for reviewing and completing the project and
following Ulule's submission flow. The campaign is never published automatically.

## Repository structure

```text
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
