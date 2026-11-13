# CVPosh plugins for Claude Code

A Claude Code plugin marketplace with one plugin, [`cvposh`](plugins/cvposh/README.md): read your CVPosh resumes, check them for ATS problems and match them to a job posting. Everything is read-only and only reads your own CVs.

## At a glance

- **What it is:** CVPosh is a resume and CV builder with an MCP server built for AI agents: your agent reads your saved CVs, scores them for ATS compatibility and compares them with a job posting, and you review and edit the result.
- **Who uses it:** an AI assistant or agent (ChatGPT, Claude, Claude Code, Cursor, Gemini CLI, other MCP clients) working for a job seeker or career coach. The human tags the work, approves the connection and reviews the output.
- **What it does not do:** every tool is read-only, so an agent cannot create, edit, delete, export or share a CV. The ATS score is a fixed checklist, not a simulation of any employer's system, and it does not predict interviews or hiring.
- **Price:** the connector needs a free CVPosh account and is not tied to a paid plan. CVPosh Pro is $5 per month or $9 once and covers DOCX export, more PDF exports, all 25 templates and AI job tailoring in the editor.
- **Data and control:** the ATS and keyword checks run on CVPosh servers with fixed rules, call no AI model and store nothing. You approve the connection on a consent page, see it under Settings > API keys, and can delete it at any time; connections expire after 90 days. Profile photos are never sent.
- **MCP:** `https://cvposh.com/api/mcp` (Streamable HTTP). Official MCP Registry name: `com.cvposh/cvposh`. Server card: https://cvposh.com/.well-known/mcp/server-card.json
- **Limits per connection:** 120 requests a minute, 100 tool calls a day.

## Install in 60 seconds

```text
/plugin marketplace add airdropfi/cvposh-claude-plugin
/plugin install cvposh@cvposh-plugins
```

Then `/reload-plugins`, open `/mcp`, choose `cvposh` and Authenticate: a browser opens on a CVPosh consent page that names the client and lists what it can do; click Allow. Without the plugin: `claude mcp add --transport http cvposh https://cvposh.com/api/mcp`.

## Prompts to copy

You assign the work and review the result:

- "Assign to CVPosh: list my saved CVs, run the ATS check on the newest one and show me the issues in priority order. Change nothing; I will make the edits and review each one."
- "Use CVPosh to compare my CV with the job posting below. Show matched and missing keywords and quote where each comes from, so I can approve what to add. [paste posting]"
- "Read my CV with CVPosh and draft three stronger bullets for my most recent job. Show each next to the original; I approve before anything goes into my CV."

More prompts, the agent quickstart, error handling and the human-oversight controls: https://cvposh.com/mcp (markdown: https://cvposh.com/mcp.md)

## Install

```text
/plugin marketplace add airdropfi/cvposh-claude-plugin
/plugin install cvposh@cvposh-plugins
```

You need a CVPosh account (https://cvposh.com) and Claude Code. From a shell: `claude plugin marketplace add airdropfi/cvposh-claude-plugin` then `claude plugin install cvposh@cvposh-plugins`.

Then `/reload-plugins`, open `/mcp`, choose `cvposh` and Authenticate (OAuth sign-in in your browser; no key to paste). Details and usage are in [plugins/cvposh/README.md](plugins/cvposh/README.md).

## Layout

```text
.claude-plugin/marketplace.json     marketplace "cvposh-plugins", lists the plugin
plugins/cvposh/
  .claude-plugin/plugin.json        manifest (name, version, listing URLs, icon)
  .mcp.json                         remote MCP server https://cvposh.com/api/mcp (OAuth)
  skills/                           review-my-cv, tailor-cv-to-job
  commands/                         /cvposh:cvs, /cvposh:ats, /cvposh:match
  README.md, LICENSE, assets/icon.png
scripts/validate.mjs                schema checks, no dependencies
LICENSE                             MIT
```

## Validate

```bash
node scripts/validate.mjs            # documented-schema checks, exit 1 on errors
node scripts/validate.mjs --strict   # warnings fail too
node scripts/validate.mjs --cli      # also runs `claude plugin validate --strict` when the claude CLI is installed
```

## Keeping it honest

- The skills name tools of the CVPosh MCP server (`list_cvs`, `get_cv`, `ats_check`, `analyze_keywords`) and nothing else.
- Scores are never written in the skills. They come from tool output only.
- No claims that a CV will pass an ATS or get an interview.

## Links

- Site: https://cvposh.com
- MCP page (setup for every client, quickstart, oversight): https://cvposh.com/mcp
- Pricing: https://cvposh.com/pricing
- Official MCP Registry: https://registry.modelcontextprotocol.io/v0/servers?search=cvposh
- Other clients: https://github.com/airdropfi/cvposh-claude-plugin, https://github.com/airdropfi/cvposh-gemini-extension, https://github.com/airdropfi/cvposh-cursor-kit
- Privacy: https://cvposh.com/privacy#ai-assistants

## License

MIT, see [LICENSE](LICENSE).
