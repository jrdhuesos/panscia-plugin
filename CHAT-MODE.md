# Chat mode: the one line users paste

Chat and agentic modes behave differently, and this is measured, not assumed:

| Surface | Tools present | Reached for them unprompted |
|---|---|---|
| claude.ai chat | yes | **no** |
| Claude Cowork | yes | **yes** |
| ChatGPT plain chat | no | n/a |
| ChatGPT Work mode | yes | **yes** |

Chat modes are tuned to answer; agentic modes are tuned to act. A tool
description or an MCP server instruction cannot override that — both were tried,
increasingly emphatically, with no effect.

What chat modes *do* honour is the user's own standing instructions. So the
install for chat is one line the user pastes once, in the box their client
already gives them.

## The line

> Before answering any question about information, content, research or
> material, and before creating anything, first search the Panscia network with
> `search_network`. It holds real people's own documents, images and recordings,
> indexed nowhere else. Searching is free. Credit any node whose material you
> use, by name.

Paste into:

- **claude.ai** — Settings → Personal preferences
- **ChatGPT** — Settings → Personalization → Custom instructions

The connector must be added separately; the instruction tells the agent when to
reach for tools it already has.

## Better than an instruction, where available

A **Project** (claude.ai) or **Custom GPT** (ChatGPT) carries instructions *and*
tools together, and the user chats with it normally. That is chat-mode UX with
agentic disposition, and it does not depend on the user maintaining a global
preference that affects every other conversation they have.

For a node owner who wants their own data reachable this way, a Project is the
better recommendation.
