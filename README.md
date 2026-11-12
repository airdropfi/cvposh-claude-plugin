# CVPosh plugins for Claude Code

A Claude Code plugin marketplace with one plugin, [`cvposh`](plugins/cvposh/README.md): read your CVPosh resumes, check them for ATS problems and match them to a job posting. Everything is read-only and only reads your own CVs.

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

## License

MIT, see [LICENSE](LICENSE).
