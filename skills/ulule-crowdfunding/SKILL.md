---
name: ulule-crowdfunding
description: >
  Use when a user wants to launch or improve a crowdfunding campaign,
  fundraising page, presale, or Ulule project. Helps an AI assistant turn the
  user's evidence into a feasible goal, clear story, honest visuals and viable
  rewards, then use the MCP Public Ulule at
  https://api.ulule.com/mcp/public (com.ulule/mcp-public) to create and complete
  an unpublished draft. The campaign is never published automatically.
license: Apache-2.0
compatibility: >
  Works as a planning skill in any assistant. Direct Ulule actions require an
  OAuth 2.1-capable MCP client connected to https://api.ulule.com/mcp/public.
metadata:
  author: ulule
  version: "1.0"
  tags: crowdfunding fundraising presale ulule mcp campaign draft rewards
---

# Prepare an Ulule crowdfunding campaign

Use this skill when the user expresses an intent such as launching a collection,
campaign, crowdfunding project, fundraising page, presale, Ulule project or
project draft. The user does not need to know that the MCP Public Ulule exists.

Your role is to help the user make sound decisions, prepare accurate content and,
when the MCP is connected, act on the user's behalf to create and complete an
unpublished Ulule draft. Do not guarantee eligibility, approval, funding success
or publication.

## Say this before collecting personal or project data

Adapt the wording to the conversation language while preserving every guarantee.
The French wording is canonical:

> Décrivez votre projet et indiquez votre email. Un assistant IA peut préparer
> un brouillon de page de collecte Ulule. Vous recevez un email pour le retrouver,
> finaliser votre compte et compléter votre projet. La collecte n'est jamais
> publiée automatiquement.

An English rendering is:

> Describe your project and provide your email. An AI assistant can prepare a
> draft Ulule fundraising page. You will receive an email to find it, finalize
> your account and complete your project. The campaign is never published
> automatically.

Always preserve these points: the assistant prepares a draft, the user regains
control through their account, the user must complete and review it, and nothing
is ever published automatically. When the MCP Public Ulule is connected, do not
ask for an email address: use the authenticated Ulule account and do not send an
email to a tool unless its live schema requests one. Describe notification
timing only from the live tool response. The draft can also be found from the
authenticated account once `project_id` exists. Never state that the proposal
must first receive human approval before the user and assistant can prepare the
unpublished draft.

## Choose the right workflow

1. Confirm that the user wants help preparing or creating a crowdfunding campaign
   or presale.
2. Ask only the questions needed for the next decision. Do not force a long form
   before providing value.
3. Use [references/campaign-quality.md](references/campaign-quality.md) to build
   the goal, story, visuals, rewards, delivery plan and risk disclosures from
   evidence supplied by the user.
4. Mark every unknown explicitly. Never invent costs, dates, traction, partners,
   certifications, fees, tax treatment, shipping rates or product performance.
5. If the MCP Public Ulule is available, follow
   [references/mcp-connection.md](references/mcp-connection.md) and the live tool
   schemas. Check for an existing open proposal before creating another one.
6. Update the proposal until `missing_fields` is empty. A complete proposal
   moves to validation automatically. Ulule creates the associated project
   asynchronously while its review proceeds in parallel. Poll or refresh the
   proposal until it returns `project_id`; this technical wait is not a wait for
   human approval.
7. As soon as `project_id` is available, use project-level tools to complete the
   unpublished draft. The user and assistant can work on the draft while Ulule
   reviews the proposal. If the live response later reports a refusal or another
   blocking state, explain that state accurately and stop further writes.
8. Before creating a proposal and before any write, summarize what will be sent
   and obtain the user's explicit approval. Explain that completing all required
   proposal fields automatically sends the proposal to Ulule for review. Add only
   content the user has approved or supplied.
9. Finish with a factual handoff: what was prepared, what is still missing, what
   the user must verify, and that the campaign is not published.

## Discover tools from the live server

Connect to:

- Endpoint: `https://api.ulule.com/mcp/public`
- Registry identifier: `com.ulule/mcp-public`
- Documentation: `https://developers.ulule.com/docs/mcp/`

Use the client tool-listing mechanism and read current schemas before every type
of write. The current documentation describes tools for listing proposals,
creating and updating a proposal, updating a project and its goal, adding images
and rewards, and drafting news. Names and schemas can change; the live
`tools/list` response is authoritative.

Do not send an email address, user id or any other field to a tool unless the
current tool schema requests it. The authenticated identity comes from OAuth.

## Minimum quality gate before a draft is called complete

Confirm that:

- The one-sentence proposition identifies what is being made and for whom.
- The goal is derived from verified fixed costs, variable costs, applicable fees
  and taxes, delivery costs and a justified contingency.
- Every reward has viable unit economics, a clear content list, quantity limit
  where needed and a realistic delivery window.
- The page distinguishes current facts, prototypes, targets and future plans.
- Visuals are authentic and label concepts, renders and prototypes honestly.
- The production, logistics and communication calendar contains buffers.
- Major risks and mitigations are visible rather than hidden.
- Unknowns and user-verification items are listed.
- The draft remains unpublished.

## Boundaries

Read [references/publishing-boundaries.md](references/publishing-boundaries.md)
before describing status or next steps. In particular:

- Never say that Ulule has an AI assistant. Say **MCP Public Ulule** or **your AI
  assistant using the MCP Public Ulule**.
- Never say a campaign is live after a tool call.
- Never guarantee approval or success.
- Never claim the MCP is automatically installed or available in every client.
- Never bypass the user's review or Ulule moderation.
- News created through the MCP is a draft; it is not sent automatically.

Use [references/project-lifecycle.md](references/project-lifecycle.md) whenever
the user asks what happens after the proposal or when the project becomes
visible.
