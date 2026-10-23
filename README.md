# 🧭 directives

A Claude Code plugin for the high-level directives you'd otherwise retype at the end of
every plan. Run `/directive <name>` in plan mode and Claude:

1. **adopts** the directive for the rest of the session,
2. **appends** it, word for word, to a `## Directives` section at the end of the plan, so
   execution inherits it after you approve the plan, and
3. **acts on it** before finalizing: it validates assumptions and asks its open questions.

## Directives

| Name | Directive |
|---|---|
| `architect` | Think and act like a principal software engineer / architect. Be thoughtful, discerning, creative, strategic, meticulous, thorough, and detail-oriented. Make no assumptions -- validate all assumptions against real code, data, and docs. Ask me any and as many questions as necessary to resolve ambiguity, gather info / context, and make critical decisions. |
| `director` | Think and act like a principal software engineer / director. Be thoughtful, generous, discerning, creative, strategic, meticulous, thorough, detail-oriented, and mindful of human emotions. Look for opportunities to improve / introduce / reduce process. Look for opportunities to foster collaboration. Look for opportunities to help individuals build and leverage their skills and interests. Make no assumptions -- validate all assumptions against real code, data, and docs. Ask me any and as many questions as necessary to resolve ambiguity, gather info / context, and make critical decisions. |

## Install

```
/plugin marketplace add jonasrmichel/directives
/plugin install directives@directives
```

Restart Claude Code. The skill shows up as `/directive`. Its fully qualified name is
`/directives:directive`, which you only need if another skill is also named `directive`.

## Usage

In plan mode, once the plan has taken shape:

```
/directive architect                          # one directive
/directive architect director                 # several, stacked
/directive architect keep the change small    # trailing text is added as an extra directive
/directive                                    # asks which directive(s) to apply
```

The plan ends with:

```markdown
## Directives

### Architect
Think and act like a principal software engineer / architect. ...

### Additional
keep the change small
```

Running a directive again replaces its entry rather than duplicating it. Outside plan mode,
`/directive <name>` just adopts the directive for the session.

The skill is user-invoked only (`disable-model-invocation: true`), so Claude never applies a
directive on its own.

## Add your own

Fork the repo and add a section to the **Directives** list at the bottom of
[`skills/directive/SKILL.md`](skills/directive/SKILL.md). The heading is the directive's
name, and the text under it is what gets copied into the plan:

```markdown
### reviewer
Review like a staff engineer: ...
```

→ `/directive reviewer`. Then install from your fork: `/plugin marketplace add <you>/directives`.

The directives live inside `SKILL.md` on purpose. Claude Code won't list or read files
outside your project without asking, so keeping everything in the one file the skill loads
means you never get permission prompts.

## Manual install (without the plugin system)

```sh
git clone https://github.com/jonasrmichel/directives.git
cp -r directives/skills/directive ~/.claude/skills/directive
```

## What this plugin runs

Markdown instructions only: no scripts, hooks, network requests, or data collection. Its
only side effect is the edit to your plan file in plan mode.

## License

MIT
