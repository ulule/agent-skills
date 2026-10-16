# Connect to the MCP Public Ulule

## Canonical identifiers

- Endpoint: `https://api.ulule.com/mcp/public`
- MCP Registry identifier: `com.ulule/mcp-public`
- Documentation: `https://developers.ulule.com/docs/mcp/`
- Transport: MCP over Streamable HTTP
- Authentication: OAuth 2.1 with dynamic client registration and PKCE

An unauthenticated endpoint request returning `401` is expected. It does not mean
the server is unavailable; the client must complete OAuth.

## Connection and discovery

Point the user's OAuth 2.1-capable MCP client to the endpoint. The client should
discover authorization metadata, register dynamically, use PKCE and show the
Ulule authorization screen. Never ask the user to paste a bearer token into the
conversation and never place a token in a URL.

After authorization:

1. Call the server's tool-listing mechanism.
2. Read each current name, description, annotations and input schema.
3. Use a read-only connection check when available.
4. Check for an existing open proposal before creating a new one.
5. Follow returned ids, states and `missing_fields`; do not infer them.

The current public documentation describes tools including `ping`,
`list_my_proposals`, `create_proposal`, `update_proposal`, `update_project`,
`update_goal`, `create_reward`, `create_project_image` and `create_news`. Treat
this list as orientation only. The live tool list and schemas are authoritative.

## Proposal-first workflow

Only `country` and `description` are required to start a proposal according to
the current documentation. The authenticated user identity comes from OAuth; do
not pass a user id or email unless the live schema explicitly requests it.

Before creating, list the user's proposals and reuse an open one where
appropriate. After creation, complete the proposal with the fields reported in
`missing_fields`. When complete, it moves to validation without a separate
submit action. Ulule's review and the preparation of the associated unpublished
draft are parallel stages; human approval of the proposal is not required before
draft work begins. A proposal can be refused, so never guarantee acceptance.

Ulule creates the project asynchronously after the proposal is complete. Refresh
or poll the proposal until the response includes `project_id`.

This is a technical wait for the identifier, not a wait for human approval.
Ulule may still be reviewing the proposal while the user and assistant complete
the unpublished draft. If the proposal remains in a non-terminal processing
state, explain that the project is still being prepared and retry later. If the
live response reports a refusal or another blocking state, report it accurately
and stop further writes.

## Writes and confirmation

Read the tool annotations. Before creating a proposal and before every write,
summarize what will be sent and obtain the user's explicit approval. Explain
that completing all required proposal fields automatically sends the proposal
to Ulule for review. Updates overwrite values. Reward and image creation can
involve external URLs; use only sources supplied or approved by the user. News
is saved as a draft and is never sent automatically.

## Fallback when the MCP is not connected

Tell the user that you can still prepare a structured brief but cannot write to
Ulule from the current client. Provide the endpoint and documentation, explain
that connecting it requires their action, and continue producing the goal,
page copy, reward table, visual brief and risk checklist in the conversation.
Do not claim that the client will discover or install the server automatically.
