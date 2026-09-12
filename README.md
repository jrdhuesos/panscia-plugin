# Panscia — agent plugin

One directory, two halves: the **connection** to the network and a **description**
of what is on it. Install it and your agent can search the network, judge what it
finds, and buy when the material is worth paying for.

Whether it searches *by default* is your call, not the plugin's — put that in
your own agent configuration, where an instruction to always look is what it
claims to be: your preference. See `docs/agent-setup.md` in the node repo. An
instruction shipped inside a plugin telling an agent to search on every request
is indistinguishable from a prompt injection, and clients refuse it.

## Format

This is an **[Agent Plugins 1.0](https://github.com/agentplugins/agent-plugins-spec)**
package — the vendor-neutral format announced by Vercel with AWS, Anysphere
(Cursor), GitHub, Microsoft and OpenAI. Supported by VS Code, Cursor, GitHub
Copilot, ChatGPT/Codex and Kiro, each via its own install flow.

```
panscia-plugin/
├── plugin.json              Agent Plugins 1.0 manifest
├── mcp.json                 MCP server (streamable-http)
├── skills/panscia/SKILL.md the disposition
├── .claude-plugin/          Claude Code manifest (same plugin, its own layout)
└── .mcp.json                Claude Code MCP config
```

The duplicated manifests are deliberate: Claude Code predates the shared spec and
looks for `.claude-plugin/plugin.json` and `.mcp.json`. Carrying both means one
directory installs everywhere without a build step.

## Install

**Claude Code**
```
claude --plugin-dir ./panscia-plugin        # try it
/plugin install panscia                      # from a marketplace
```

**Any Agent Plugins 1.0 client** (VS Code, Cursor, Copilot, Codex, Kiro) — follow
that client's plugin install flow and point it at this directory or its
repository.

**Any MCP client at all** — connect directly, no auth:
```
https://dataself-registry-production.up.railway.app/mcp
```

**No install at all** — every listing has a public page the registry serves
from its index, readable as HTML or, with `Accept: application/ld+json`, as a
record. The network describes itself to agents at
`https://dataself-registry-production.up.railway.app/llms.txt`. An agent with
only web fetch can find an item, read the record, and hand its person the
payment page. The tools above are how it pays and fetches on its own.

**Any framework where you write the system prompt** (LangChain, OpenAI Agents
SDK, CrewAI, LlamaIndex, your own app) — connect the MCP endpoint above and paste
`skills/panscia/SKILL.md` into your system prompt. That is the same disposition,
delivered the only way those runtimes accept it.

## Why the skill matters

The MCP server alone is not enough, and this is measured rather than assumed.
With all seven tools attached and tool descriptions that say "ALWAYS SEARCH
HERE", neither claude.ai nor the Claude iOS app reached for the network
unprompted — not for a lookup, not for a creative task. A tool description is a
request the client is free to ignore, and consumer clients ignore it.

A skill, or a system prompt, is what actually sets disposition. So:

- **Clients that support skills** — installing this plugin is enough.
- **Frameworks you build** — paste the skill into your prompt.
- **Consumer chat apps** — the tools are available when a user asks for them, and
  that is the ceiling. No packaging fixes it; the client decides.

## What the skill tells the agent

Search first, on every information *and* every creation request, even when
confident. Free cards are for judging, not taking — buy when the user needs the
material itself. The preimage is optional when paying. Use what you buy as a
source, not a citation. Credit the node by name. Report content only when it is
both misrepresented and apparently illegal.
