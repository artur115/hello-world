# Claude Code add-ons for this repo

Setup based on the reel "4 plugins to install before you vibe-code" (alex.proreels).

| Tool | What it does | Status in this repo |
|------|--------------|---------------------|
| [Ponytail](https://github.com/DietrichGebert/ponytail) | "Lazy senior dev" mode: pushes the agent toward the smallest solution that works | Plugin enabled in `.claude/settings.json` |
| [Agent Skills](https://github.com/addyosmani/agent-skills) (Addy Osmani) | 25 engineering skills plus `/spec` `/plan` `/build` `/test` `/review` `/ship` commands | Plugin enabled in `.claude/settings.json` |
| [Graphify](https://github.com/Graphify-Labs/graphify) | Builds a code knowledge graph so the agent queries it instead of re-reading files | Skill in `.claude/skills/graphify`, hooks in `.claude/settings.json`, graph in `graphify-out/` |
| [OmniRoute](https://github.com/cheaper-inference/OmniRoute) | Local AI gateway that reroutes Claude Code to other (free) providers | **Not installed.** Optional, see below |

## On your Mac

```bash
# 1. Graphify CLI (needed by the hooks in .claude/settings.json)
uv tool install graphifyy        # or: pipx install graphifyy

# 2. Open the repo in Claude Code. It will offer to install the two plugins
#    declared in .claude/settings.json; accept. Manual equivalent:
#    /plugin marketplace add DietrichGebert/ponytail
#    /plugin install ponytail@ponytail
#    /plugin marketplace add addyosmani/agent-skills
#    /plugin install agent-skills@addy-agent-skills
```

Then, inside Claude Code: `/graphify .` builds the full graph (`graphify update .` rebuilds the code part without any API calls), and `/spec` → `/plan` → `/build` → `/test` → `/review` → `/ship` is the Agent Skills workflow.

## OmniRoute (optional, read first)

OmniRoute runs a local proxy (`http://localhost:20128`) and sends your Claude Code traffic to whichever provider it picks, such as Gemini, DeepSeek or Kimi. Things to know:

- Every prompt and every file Claude reads passes through it and on to third-party providers.
- Answers come from other models, not Claude, and quality varies between them.
- Free tiers come with their own terms and rate limits, and some providers train on free-tier traffic.

If you still want it:

```bash
npx omniroute                    # starts the dashboard on localhost:20128
omniroute run claude             # launch Claude Code through it
```
