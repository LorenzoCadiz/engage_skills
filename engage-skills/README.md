# 🚫 REPLACED: engage-skills → tdx-skills:engage

**This directory has been completely replaced. Use `tdx-skills:engage` instead.**

## Breaking Change Notice

The entire `engage-skills` directory has been removed and replaced with the enhanced `tdx-skills:engage` skill. This is a breaking change with immediate effect.

## Technical Issues That Led to Replacement

The previous engage-skills implementation had several critical issues:

### 1. Repository Hygiene Issues
- **6 .DS_Store files committed**: The .gitignore entry was added but already-committed files needed `git rm --cached` to remove from tracking
- Poor Git practices affecting repository quality

### 2. Architectural Boundary Violations
- **journey/SKILL.md changes were too invasive** (+85 lines)
- The "Email Activation Patterns" section embedded email-specific content into the journey skill, which owns CDP journey orchestration — not email patterns
- Referenced non-existent skills: `email-template-creator`, `email-campaign-orchestration`
- **Scope creep**: Engage was incorrectly expanding into journey territory when it should only impact activation steps with Engage connection types

### 3. Incorrect YAML Structure
- **email-journey-builder YAML structure was wrong**:
  - `email:` block with `template_id`/`sender_id` doesn't match actual `tdx journey` YAML format
  - Journey activations use `activation: key-name` referencing the `activations:` section
  - Duration format `"2d"` was incorrect — journeys use `duration: 2` + `unit: day`
- Heavy duplication of existing `tdx-skills/journey` skill functionality

### 4. Over-Engineering
- **Bloated bash functions throughout**: Skills guide Claude on tool usage — they're not shell script libraries
- Functions like `create_welcome_journey`, `validate_journey`, `cleanup_unused_templates`, `check_template_usage` added token cost without effective guidance
- Violated CLAUDE.md principles: "Show, don't explain" and keep skills concise
- Only `engage-deliverability` (138 lines) and `engage-utm` (137 lines) achieved appropriate conciseness

### 5. Workflow Misalignment
- Used outdated CLI patterns (`tdx engage campaign create`) instead of modern YAML-first workflow
- Fragmented approach across multiple skills instead of unified workflow
- Missing critical modern features (validation pipeline, parent segment integration)

## Migration Guide

### Direct Replacements

| ❌ Old (Removed) | ✅ New Replacement |
|------------------|-------------------|
| All engage-skills/* | `tdx-skills:engage` |
| `email-journey-builder` | `tdx-skills:journey` + engage activations |
| `email-testing-validator` | `tdx-skills:engage` (built-in validation) |
| `engage-deliverability` | `tdx-skills:engage` (deliverability section) |
| `engage-sender` | `tdx-skills:engage` (sender configuration) |
| `engage-utm` | `tdx-skills:engage` (UTM section) |

### Key Improvements in Replacement

✅ **Modern YAML-first workflow** (not CLI commands)
✅ **Unified template + campaign management**
✅ **Proper architectural boundaries** (Engage vs Journey separation)
✅ **Correct YAML structure** matching actual TD APIs
✅ **Concise, token-efficient guidance** (not bash libraries)
✅ **Complete validation pipeline** (validate → dry-run → push)
✅ **Parent segment integration**

## Quick Start with New Skill

```bash
# Modern YAML-first workflow:
# 1. Write YAML + HTML files together
# 2. Validate automatically
# 3. Push with dry-run
# 4. Deploy with --yes

# Use: tdx-skills:engage
# Instead of: fragmented engage-skills/*
```

## Architecture Clarity

**Engage Scope**: Templates, campaigns, sender setup, deliverability
**Journey Scope**: Stages, decision points, waits, merges, orchestration
**Boundary**: Engage only affects activation steps with Engage connection types

The enhanced `tdx-skills:engage` respects these boundaries and integrates properly with `tdx-skills:journey`.

---

**No backward compatibility is provided.** Switch to `tdx-skills:engage` immediately.