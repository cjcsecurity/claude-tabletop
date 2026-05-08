# Install

These skills install at the **user level** by default — they work in any project folder you `cd` into. You can also install them at the project level if you'd rather scope them per-repo.

## User-level install (recommended)

Works for any project on your machine.

### Option A — copy

```bash
git clone https://github.com/cjcsecurity/claude-tabletop.git
cp -r claude-tabletop/skills/tabletop-exercise ~/.claude/skills/
cp -r claude-tabletop/skills/tabletop-aar      ~/.claude/skills/
```

### Option B — symlink (recommended if you plan to update from `git pull`)

```bash
git clone https://github.com/cjcsecurity/claude-tabletop.git ~/code/claude-tabletop
ln -s ~/code/claude-tabletop/skills/tabletop-exercise ~/.claude/skills/tabletop-exercise
ln -s ~/code/claude-tabletop/skills/tabletop-aar      ~/.claude/skills/tabletop-aar
```

`git pull` in `~/code/claude-tabletop` and your installed skills update automatically.

## Project-level install

Use when you want the skills available only inside a specific repo (e.g. an internal security toolkit you don't want to leak to other projects).

```bash
mkdir -p .claude/skills
cp -r /path/to/claude-tabletop/skills/tabletop-exercise .claude/skills/
cp -r /path/to/claude-tabletop/skills/tabletop-aar      .claude/skills/
```

The `.claude/skills/` directory at the repo root is the project-level skills location.

## Verify install

Open Claude Code in any project folder and type `/`. You should see `tabletop-exercise` and `tabletop-aar` in the skills list. If not:

- Confirm files are at `~/.claude/skills/tabletop-exercise/SKILL.md` and `~/.claude/skills/tabletop-aar/SKILL.md`
- Restart Claude Code (skill registration happens at session start)
- Check the skill descriptions render — `cat ~/.claude/skills/tabletop-exercise/SKILL.md | head -5` should show valid YAML frontmatter

## Uninstall

```bash
rm -rf ~/.claude/skills/tabletop-exercise ~/.claude/skills/tabletop-aar
```

## Updating

If you used the symlink install: `git -C ~/code/claude-tabletop pull`. Done.

If you copied: `git pull && cp -r skills/tabletop-exercise ~/.claude/skills/ && cp -r skills/tabletop-aar ~/.claude/skills/`.
