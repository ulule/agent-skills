# Ulule Agent Skills

Official Ulule Agent Skills for crowdfunding, fundraising projects and presales.

This repository helps compatible AI assistants understand Ulule workflows, prepare project proposals and drafts, structure funding goals and rewards, and connect to the public Ulule MCP server.

## Available skills

### `ulule-crowdfunding`

Use this skill when a user wants to create, prepare, edit or recover an Ulule crowdfunding campaign, fundraising project or presale. The user does not need to mention MCP or an AI assistant.

The skill helps an assistant to:

- Recognize crowdfunding, fundraising and presale intents.
- Gather a structured project brief.
- Prepare a proposal with a project description, goal and rewards.
- Find and update an existing proposal instead of creating duplicates.
- Distinguish between a proposal, an unpublished project draft and a live campaign.
- Connect to Ulule through the public MCP server when supported by the client.

## Public Ulule MCP

The public Ulule MCP endpoint is:

```text
https://api.ulule.com/mcp/public
```

Documentation:

<https://developers.ulule.com/docs/mcp/>

The server uses OAuth 2.1. Compatible MCP clients should handle authorization, dynamic client registration and PKCE. Never paste an access token into a conversation.

## Publication boundaries

The skill helps creators prepare and edit their project. It does not publish a campaign automatically, guarantee approval or replace Ulule's moderation process.

Always keep these stages separate:

1. Project proposal.
2. Unpublished project draft.
3. Live campaign.

The creator remains responsible for reviewing the content, completing the project and following Ulule's publication process.

## Repository structure

```text
skills/
└── ulule-crowdfunding/
    ├── SKILL.md
    └── references/
        ├── mcp-connection.md
        ├── project-lifecycle.md
        └── publishing-boundaries.md
```

## License

Apache-2.0. See [LICENSE](LICENSE).
