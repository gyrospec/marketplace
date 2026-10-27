# Gyrospec marketplace

The plugin marketplace for [Gyrospec](https://github.com/gyrospec/skills). It lists two plugins, both built from `gyrospec/skills`:

- **`gyrospec`**: the Gyrospec local mode skills: discovery, PRD, prototype, spec, breakdown, writing plans, and executing plans, with gates you approve, plus the offline `gyro` script.
- **`gyrospec-upstream-skills`**: Matt Pocock's skills from [mattpocock/skills](https://github.com/mattpocock/skills) (MIT), as kept in the Gyrospec fork: the upstream skills the Gyrospec phases call (`grilling`, `prototype`, `tdd`, `code-review`, `domain-modeling`, `codebase-design`), from the same repository.

Install both. Every agent also needs **Node 20 or later**, because the skills run `gyro.mjs` with `node`.

## Where it installs

| Agent | How | Updates | Tested |
|---|---|---|---|
| Claude Code | This marketplace | `/plugin marketplace update gyrospec` | Yes |
| Codex | This marketplace | `codex plugin marketplace upgrade gyrospec` | Yes |
| GitHub Copilot CLI | This marketplace | Copilot's marketplace update | Not yet |
| Gemini CLI | `gemini skills install` (copies folders) | Re-run the install | Not yet |
| Any other agent that reads Agent Skills folders (`SKILL.md`) | Copy the folders | Copy again | The Codex copy route is tested |

Pick one route per agent. A plugin install and a folder copy in the same agent give you every skill twice.

### Claude Code

```text
/plugin marketplace add gyrospec/marketplace
/plugin install gyrospec@gyrospec
/plugin install gyrospec-upstream-skills@gyrospec
```

The same from a terminal:

```bash
claude plugin marketplace add gyrospec/marketplace
claude plugin install gyrospec@gyrospec
claude plugin install gyrospec-upstream-skills@gyrospec
```

Start a new session afterwards. The phase skills are typed by you (`/gyro-discovery` to `/gyro-executing-plans`); the model reaches the `gyro` reference skill itself.

### Codex

```bash
codex plugin marketplace add gyrospec/marketplace
codex plugin add gyrospec@gyrospec
codex plugin add gyrospec-upstream-skills@gyrospec
```

On Windows, keep `CODEX_HOME` on a short path: Codex clones the plugin repository there, and a very long path fails with `Filename too long`.

### GitHub Copilot CLI (not tested yet)

Copilot reads the same marketplace format. This should work, but nobody has run it against Gyrospec yet:

```bash
copilot plugin marketplace add gyrospec/marketplace
copilot plugin install gyrospec@gyrospec
copilot plugin install gyrospec-upstream-skills@gyrospec
```

### Gemini CLI (not tested yet)

Gemini installs skill folders by bucket. Gyrospec's skills are one bucket; the upstream skills it calls live in two more:

```bash
gemini skills install https://github.com/gyrospec/skills.git --path skills/gyrospec
gemini skills install https://github.com/gyrospec/skills.git --path skills/engineering
gemini skills install https://github.com/gyrospec/skills.git --path skills/productivity
```

### Any other agent: copy the folders

Clone `gyrospec/skills` and copy each folder below, whole, into the agent's skills directory (for Codex without plugins that is `~/.agents/skills`):

- the eight folders under `skills/gyrospec/`: `gyro`, `gyro-discovery`, `gyro-prd`, `gyro-prototype`, `gyro-spec`, `gyro-breakdown`, `gyro-writing-plans`, `gyro-executing-plans`
- `skills/productivity/grilling`
- `skills/engineering/prototype`, `tdd`, `code-review`, `domain-modeling`, `codebase-design`

Keep `gyro/scripts/` (the `gyro.mjs` bundle and its licenses) and each `NOTICE.md` with their folders. See the [gyrospec README](https://github.com/gyrospec/skills/blob/main/skills/gyrospec/README.md) for what each skill does.

## Updates

Both plugins come from `gyrospec/skills` on its default branch. A release raises `version` in `skills/gyrospec/.claude-plugin/plugin.json`; agents that install from this marketplace pick it up after a marketplace update. Copied folders do not update themselves: copy them again.
