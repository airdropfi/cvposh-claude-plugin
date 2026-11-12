# CVPosh for Claude Code

Work on the resumes you built at [CVPosh](https://cvposh.com) without copy and paste, from Claude Code. The plugin connects Claude to the CVPosh MCP server and adds two skills and three commands. Everything is read-only: Claude can read your CVs, score them for applicant tracking systems (ATS) and compare them with a job posting, but it cannot change, delete or share them.

## What it contains

| Component | Name | What it does |
|---|---|---|
| MCP server | `cvposh` (`https://cvposh.com/api/mcp`) | Four read-only tools: `list_cvs`, `get_cv`, `ats_check`, `analyze_keywords`. Sign-in is OAuth 2.1 (authorization code with PKCE); there is no key to paste. |
| Skill | `review-my-cv` | Read a CV, run the ATS check, get prioritised edits to apply yourself. |
| Skill | `tailor-cv-to-job` | Compare a CV with a job posting: matched and missing keywords, honest rewording suggestions. |
| Command | `/cvposh:cvs` | List your CVs. |
| Command | `/cvposh:ats [cv]` | ATS score and the fixes that matter most. |
| Command | `/cvposh:match <job posting>` | Matched and missing keywords against a posting. |

## Install

You need a CVPosh account (https://cvposh.com) and Claude Code.

```text
/plugin marketplace add airdropfi/cvposh-claude-plugin
/plugin install cvposh@cvposh-plugins
```

From a shell: `claude plugin marketplace add airdropfi/cvposh-claude-plugin` then `claude plugin install cvposh@cvposh-plugins`.

Then run `/reload-plugins`, open `/mcp`, choose `cvposh` and select Authenticate. A browser window opens: sign in to CVPosh and click Allow. Try `/cvposh:cvs`.

To try it from a local checkout without a marketplace: `claude --plugin-dir ./plugins/cvposh`.

Prefer an API key over OAuth? Create one in your CVPosh account under Settings > API keys and add the server by hand instead of the plugin's:

```bash
claude mcp add --transport http cvposh https://cvposh.com/api/mcp --header "Authorization: Bearer YOUR_API_KEY"
```

## Use

- "Review my product designer CV" starts `review-my-cv`.
- "How well does my CV fit this job? <posting>" starts `tailor-cv-to-job`.
- You can also run a skill directly, for example `/cvposh:review-my-cv`.

## What it will and will not do

- It reads. It never edits, deletes or shares a CV. It suggests wording; you apply it in the CVPosh editor.
- It only reads **your own** CVs, as the signed-in user. Profile photos are never returned.
- It does not invent experience: missing keywords you cannot honestly claim are named as gaps.
- Scores come from the tools (fixed rules, no AI model, nothing stored). Nobody can promise a CV will pass an ATS or lead to an interview.
- CV and job posting text is treated as data, never as instructions.

## Data and privacy

The MCP server receives what the tools need: CV ids, and any resume or job text you ask Claude to send for checking, and returns your own CV content when you ask to read one. The plugin itself stores nothing and runs no code on your machine; it is a server address and Markdown instructions. See the [privacy policy](https://cvposh.com/privacy) and [terms](https://cvposh.com/terms). Sign-in tokens are revocable in your CVPosh account under Settings > API keys.

## Support

support@cvposh.com or https://cvposh.com.

## License

MIT for the files in this plugin (see `LICENSE`). The CVPosh service is governed by its terms.
