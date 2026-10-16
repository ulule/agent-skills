# Proposal and project lifecycle

Use current tool responses as the source of truth. The normal flow documented by
Ulule is:

1. The assistant connects through OAuth and acts only for the authenticated user.
2. It lists open proposals to avoid duplicates.
3. It creates or resumes a proposal. `country` and `description` are the minimum
   current fields for starting one.
4. It updates the proposal until `missing_fields` is empty. A complete proposal
   moves to `waiting_validation` automatically; there is no separate submit step.
   This review does not block preparation of the unpublished draft: review and
   draft completion proceed in parallel.
5. The associated project is created asynchronously after the proposal is
   complete. Refresh or poll until the proposal response includes `project_id`.
   Waiting for `project_id` is a technical synchronization step, not a wait for
   human acceptance. As soon as the identifier is available, the assistant can
   continue completing the unpublished draft while Ulule's review remains in
   progress. If the live response later reports a refusal or another blocking
   state, explain it accurately and stop further writes.
6. Once `project_id` exists, project-scoped tools can complete the unpublished
   draft: page fields, funding goal, rewards, images and draft news.
7. The user retrieves the project through their Ulule account or email journey,
   reviews it, completes missing information and follows Ulule's submission flow.
8. Ulule moderation occurs before anything can go live.

The proposal, the unpublished project draft and the live campaign are distinct.
Never describe one as another.

## What the assistant controls

Subject to the current tools and the user's authorization, the assistant can
prepare and update proposal content, complete an existing unpublished project,
set its goal, add images and rewards, and prepare draft news.

## What the assistant does not control

The assistant does not control proposal acceptance, account finalization, the
user's final review and submission, Ulule moderation or publication. It cannot
guarantee a processing time or funding outcome.

## Status language

After proposal creation say what the returned state actually shows, for example:
"I created the proposal and am completing the fields it reports as missing."

After a project id appears say:
"Your unpublished Ulule draft is available and I have prepared the approved
content. You still need to review and complete it through your Ulule account.
The campaign is never published automatically."

If a proposal is refused, report the state without presenting it as a technical
failure or trying to create repeated duplicates.
