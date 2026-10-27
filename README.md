# Gyrospec marketplace

The Claude Code marketplace for [Gyrospec](https://github.com/gyrospec/skills). It lists two plugins, both built from `gyrospec/skills`:

- `gyrospec`: the Gyrospec local mode skills (`skills/gyrospec`): discovery, PRD, prototype, spec, breakdown, writing plans, and executing plans, with gates you approve, plus the offline `gyro` script. Node 20 or later is required.
- `mattpocock-skills`: the upstream skills the Gyrospec phases call (`grilling`, `prototype`, `tdd`, `code-review`, `domain-modeling`, `codebase-design`), from the same repository.

## Install

```text
/plugin marketplace add gyrospec/marketplace
/plugin install gyrospec@gyrospec
/plugin install mattpocock-skills@gyrospec
```

## Update

Plugins come from `gyrospec/skills` on its default branch. After a release there (the plugin's `version` in `skills/gyrospec/.claude-plugin/plugin.json` is raised), run:

```text
/plugin marketplace update gyrospec
```

then update the plugins from `/plugin`.

Codex installs the skill folders directly; see the [gyrospec README](https://github.com/gyrospec/skills/blob/main/skills/gyrospec/README.md).
