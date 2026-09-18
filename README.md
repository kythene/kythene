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

There is a second, optional server for looking after the workspace itself -
share codes, the workspace guide, moving knowledge between workspaces:

```
https://kythene.com/mcp/kythene-manage
```

Add it as a second entry if you want it. Most people never do: keeping it
separate means the everyday surface stays small, and every tool a client mounts
sits in its context in every session whether it is used or not.

## Tools

Kythene exposes **43** MCP tools: **38** on the
endpoint above and **8** on the optional management server (a few
sit on both). This list is generated from the running server, so it is exactly
what the current release ships:

- **`approve`** - Approve (approved=true) or reject (approved=false, note required) a collection or artifact at its current revision/version.
- **`brief`** - Open a session with ONE call instead of four.
- **`catch_up`** - See what changed since your instance last looked - call this at the START of a session to open caught up.
- **`comment`** - Comment on a collection or artifact; the comment pins to its current revision/version.
- **`create_collection`** - Create a collection from one or more artifacts - make work known to the space (kythe it).
- **`create_page`** - Add a page to a wiki, as a DRAFT - nobody can read it, and it is in no search or recall, until you publish it with set_page_state.
- **`create_share_code`** - Mint a share code for a tag (a label or a project) - a private link for someone outside the space.
- **`create_wiki`** - Create a wiki in this workspace: a tree of pages your team reads in Kythene.
- **`deprecate`** - Mark a memory stale by id so recall stops surfacing it (instances stop applying it), while it stays retrievable for audit - prefer this over forget when…
- **`edit_collection`** - Edit a collection's membership without republishing (which would create a new collection and abandon its comments and history).
- **`end_review`** - Take a collection out of review once you are done - the clean exit that complements set_review.
- **`forget`** - Permanently remove a memory by id.
- **`get_artifact`** - Get an artifact's metadata and version history; set include_content to fetch the bytes of a version (0 = latest).
- **`get_collection`** - Get a collection with its member artifacts and tags.
- **`get_inbox`** - Feedback on your publishes since a time (comments, approvals, rejections).
- **`get_page`** - Read one page: its markdown `body`, its `state`, what links to it (`links_here` - who depends on it, which is what matters before you change something) and…
- **`get_presence`** - Who is working on what right now (last 30 minutes), with areas touched by more than one instance flagged as conflicts.
- **`get_usage`** - How this workspace is being used over a window (default 30 days): recall volume and the zero-result rate (the share of recalls that came back empty - the…
- **`get_workspace_guide`** - Read this workspace's operating manual: the house rules for writing here (style, tag taxonomy, memory vs collection, what belongs and what does not).
- **`link_memory`** - Create or remove a link between two memories over the from_id -> to_id edge.
- **`list_collections`** - List the collections visible in your space, newest first.
- **`list_pages`** - Walk a wiki's tree: every page you can see, parent before child, with its `path`, its `state` and its `depth`.
- **`list_pending`** - Your personal inbox across ALL your workspaces (#126): items addressed to YOU - approvals/rejections and comments on your work, block feedback, and memories…
- **`list_projects`** - List the projects (project-kind tags) in the space - the valid `project` values for recall, remember and publish.
- **`list_readers`** - Which instances read a collection or artifact (lineage).
- **`list_share_codes`** - List share codes. *(management server)*
- **`list_spaces`** - Your member spaces - the valid share targets.
- **`list_wikis`** - List the wikis in a workspace, with what each is for, how many pages it holds, how many of those are published, and when anything in it last went live - enough…
- **`move_page`** - Move a page under a different `parent`, rename its `slug`, or both.
- **`promote_memory`** - Promote a memory into another workspace you belong to (from a private/personal workspace to a team). *(management server)*
- **`push_version`** - Push a new version of an existing artifact.
- **`recall`** - Recall the most relevant context, with full content, in one call.
- **`remember`** - Store a memory (markdown body).
- **`report_activity`** - Report what you are working on (areas: file paths, modules, topics).
- **`resolve_project`** - Map a working directory to the Kythene project(s) it belongs to, so you can brief and recall for the right project without a human naming it.
- **`review_block`** - Flag one block of a renderable artifact and optionally comment on it - the block-level equivalent of comment/approve.
- **`revoke_share_code`** - Revoke a share code by id (from list_share_codes). *(management server)*
- **`set_collection_state`** - Move a collection through its lifecycle by naming the target `state`: "archived" archives a live collection (a reversible retirement that hides it from the…
- **`set_page_state`** - Move a page through its lifecycle by naming the target `state`: "published" makes the newest version the one readers see, and puts it into search and recall…
- **`set_review`** - Turn the approval-review flow on or off for an existing collection (requested=true to request review, false to cancel).
- **`set_workspace_guide`** - Replace this workspace's operating manual with `body` (markdown), and return the updated guide. *(management server)*
- **`share_collection`** - Map a collection into another space you belong to (e.g. a shared client space), or remove that mapping. *(management server)*
- **`update_page`** - Replace a page's body with `body`, in FULL - this is not an append.


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
