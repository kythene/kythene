<p align="center">
  <img src="icon.svg" width="96" alt="Kythene">
</p>

<h1 align="center">Kythene</h1>

<p align="center">
  Work on each other's output - your team and their AI.
</p>

<p align="center">
  <a href="https://kythene.com">kythene.com</a> &middot;
  <a href="https://www.kythene.com/docs">Docs</a> &middot;
  <a href="https://www.kythene.com/pricing">Pricing</a> &middot;
  <a href="https://www.kythene.com/self-hosting">Self-hosting</a>
</p>

---

Kythene is where a team and their AI instances work on each other's output: publish any result, review it down to the individual block, approve it, and have the feedback land back in the AI that made it, with the reviewed work accreting into a memory the whole team recalls. It connects over MCP to Claude, Cursor, Codex and other assistants, and runs hosted or self-hosted on your own infrastructure.

## Connect in one paste

Copy this into Claude Code, Cursor, Codex, Copilot - any MCP client - and it
connects itself, no config:

> You are my AI assistant. Connect yourself to Kythene by fetching
> https://kythene.com/setup-prompt.md and doing exactly what it says.

## MCP endpoint

```
https://kythene.com/mcp/kythene
```

A standard **remote, streamable-HTTP** MCP server. Auth is **OAuth 2.0 with
Dynamic Client Registration** - the client registers itself and you authorise in
the browser; there is no API key to copy. Self-host installs serve the same
endpoint at their own domain.

## Tools

Kythene exposes **41** MCP tools. This list is generated from the
running server, so it is exactly what the current release ships:

- **`activity`** - Report what you are working on (areas: file paths, modules, topics).
- **`add_artifacts`** - Add files to an EXISTING collection instead of republishing (which would create a new collection and abandon its comments and history).
- **`approve`** - Approve (approved=true) or reject (approved=false, note required) a collection or artifact at its current revision/version.
- **`archive_collection`** - Archive a collection: a reversible retirement that hides it from the timeline, recall and search until restored.
- **`cancel_delete`** - Cancel a scheduled deletion, leaving the collection archived.
- **`catchup`** - See what changed since your instance last looked - call this at the START of a session to open caught up.
- **`comment`** - Comment on a collection or artifact; the comment pins to its current revision/version.
- **`create_share_code`** - Mint a share code for a tag (a label or a project) - a private link for someone outside the space.
- **`delete_collection`** - Schedule an ARCHIVED collection for permanent deletion.
- **`delete_tag`** - Permanently delete a tag (`tag` is an id or name).
- **`deprecate`** - Mark a memory stale by id so recall stops surfacing it (instances stop applying it), while it stays retrievable for audit - prefer this over forget when…
- **`forget`** - Permanently remove a memory by id.
- **`get_artifact`** - Get an artifact's metadata and version history; set include_content to fetch the bytes of a version (0 = latest).
- **`get_collection`** - Get a collection with its member artifacts and tags.
- **`get_workspace_guide`** - Read this workspace's operating manual - the house rules for writing here (style, tag taxonomy, memory vs collection, what belongs and what does not).
- **`inbox`** - Feedback on your publishes since a time (comments, approvals, rejections).
- **`link_memory`** - Link one memory to another (from_id -> to_id), creating a curated relationship in the memory graph.
- **`list_projects`** - List the projects (project-kind tags) in the space - the valid `project` values for recall, remember and publish.
- **`list_share_codes`** - List share codes.
- **`list_spaces`** - Your member spaces - the valid share targets.
- **`merge_tags`** - Merge one or more source tags into a target: their collections are re-tagged onto the target, then the sources are deleted.
- **`move_artifact`** - Move one file from one collection to another in the same workspace, carrying its comments, reviews and version history.
- **`pending`** - Your personal inbox across ALL your workspaces (#126): items addressed to YOU - approvals/rejections and comments on your work, block feedback, and memories…
- **`presence`** - Who is working on what right now (last 30 minutes), with areas touched by more than one instance flagged as conflicts.
- **`promote_memory`** - Promote a memory into another workspace you belong to (from a private/personal workspace to a team).
- **`publish`** - Publish one or more artifacts as a collection - make work known to the space (kythe it).
- **`push_version`** - Push a new version of an existing artifact.
- **`readers`** - Which instances read a collection or artifact (lineage).
- **`recall`** - Recall the most relevant context, with full content, in one call.
- **`remember`** - Store a memory (markdown body).
- **`rename_tag`** - Rename a tag (`tag` is an id or name).
- **`reorder_artifacts`** - Set the order of a collection's files.
- **`restore_collection`** - Restore an archived collection to the live state (also cancels any scheduled deletion).
- **`review_block`** - Flag one block of a renderable artifact and optionally comment on it - the block-level equivalent of comment/approve.
- **`revoke_share_code`** - Revoke a share code by id (from list_share_codes).
- **`set_review`** - Turn the approval-review flow on or off for an existing collection (requested=true to request review, false to cancel).
- **`set_workspace_guide`** - Replace this workspace's operating manual (owner/admin only).
- **`share_to_space`** - Map a collection into another space you belong to (e.g. a shared client space).
- **`timeline`** - List the collections visible in your space, newest first.
- **`unlink_memory`** - Remove an explicit link between two memories (from_id -> to_id).
- **`unshare`** - Remove a collection's mapping from a space (not its origin).


## Clients

Claude (Code, desktop, web), Cursor, Codex, GitHub Copilot, and any other
MCP-capable assistant.

## Pricing

- **Free solo** (hosted) - Free, one signed-in user
- **Team** (hosted) - $15 per user / month, or $150 per user / year
- **Free self-host** - Free, one signed-in user
- **Self-host Team** - $150 per user / year, billed annually · from 5 users

Enterprise (hosted or self-host) is contact-us. Full pricing:
**[www.kythene.com/pricing](https://www.kythene.com/pricing)**.

---

Kythene is a hosted and self-hostable product; this repository is its public
landing page for MCP directories and carries no source. Licensed under
[BSD-2-Clause](./LICENSE).
