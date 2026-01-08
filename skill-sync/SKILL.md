---
name: skill-sync
description: Automatically sync skills to the ClaudeSkills backup folder. Use this skill after creating or updating any skill in this project to keep the backup folder in sync.
allowed-tools: Bash, Read, Write, Glob
---

# Skill Sync

This skill ensures all skills created or updated in the Ential project are automatically synced to the central ClaudeSkills backup folder.

## Target Locations

- **Source:** `/Users/ryandrake/Documents/Coding/Dev/Ential/.claude/skills/`
- **Backup:** `/Users/ryandrake/Documents/Coding/dev/ClaudeSkills/`

## When to Use

This skill should be triggered automatically whenever:
1. A new skill is created in this project
2. An existing skill is updated/modified
3. The user explicitly asks to sync skills

## Sync Process

### For New Skills

When creating a new skill:
1. Create the skill in the Ential project at `.claude/skills/<skill-name>/SKILL.md`
2. Immediately copy the entire skill folder to the ClaudeSkills backup:
   ```bash
   cp -r /Users/ryandrake/Documents/Coding/Dev/Ential/.claude/skills/<skill-name> /Users/ryandrake/Documents/Coding/dev/ClaudeSkills/
   ```

### For Updated Skills

When updating an existing skill:
1. Make the changes to the skill in the Ential project
2. Sync the updated skill to the backup:
   ```bash
   cp -r /Users/ryandrake/Documents/Coding/Dev/Ential/.claude/skills/<skill-name> /Users/ryandrake/Documents/Coding/dev/ClaudeSkills/
   ```

### Full Sync (All Skills)

To sync all skills at once:
```bash
cp -r /Users/ryandrake/Documents/Coding/Dev/Ential/.claude/skills/* /Users/ryandrake/Documents/Coding/dev/ClaudeSkills/
```

## Important Rules

1. **Always sync after skill changes** - Never leave the backup out of date
2. **Preserve folder structure** - Each skill should maintain its folder structure (`<skill-name>/SKILL.md`)
3. **Include all files** - If a skill has additional files (templates, examples), sync those too
4. **Verify sync** - After syncing, optionally verify the backup matches the source

## Verification Command

To verify skills are in sync:
```bash
diff -rq /Users/ryandrake/Documents/Coding/Dev/Ential/.claude/skills/ /Users/ryandrake/Documents/Coding/dev/ClaudeSkills/
```

## Integration with Other Skills

When using skills that create or modify skills (like `compound-engineering:skill-creator` or `compound-engineering:create-agent-skills`), this sync process should be performed as a final step.
