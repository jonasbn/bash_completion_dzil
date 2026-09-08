# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this is

A single Bash completion script for [`dzil`](http://dzil.org/) (Dist::Zilla). The
entire deliverable is the file `dzil` at the repo root — a shell fragment that is
sourced (not executed) into a user's Bash session. There is no build step and no
runtime test suite; everything else in the repo is documentation and lint config.

## Architecture

`dzil` defines one function, `_dzil`, registered via `complete -F _dzil dzil`.

- Top-level command completions are **generated dynamically** at completion time
  by running `dzil commands` and stripping descriptions with `sed`. This is why
  installed `Dist::Zilla::App::Command::*` plugins are picked up automatically —
  no list is hardcoded.
- Sub-command option flags **are** hardcoded, in `if`/`elif` branches that match
  `${prev}`. Currently only `listdeps` and `authordeps` have such branches.
- To add option completions for another sub-command, add an `elif [[ "${prev}"
  == "..." ]]` branch that sets a local `opts` and fills `COMPREPLY` via
  `compgen -W`.

Note the existing `listdeps` / `authordeps` branch logic overlaps (the second
condition tests `listdeps` again, which the first branch already returns on) —
preserve intent if refactoring.

## Validation

CI runs on every push via four independent GitHub Actions workflows in
`.github/workflows/`. Run the equivalent locally before committing:

| Check | Local command | Config |
|-------|---------------|--------|
| ShellCheck | `shellcheck dzil` | `.shellcheckrc` disables SC2148, SC2207, SC2086 |
| EditorConfig | `editorconfig-checker` | `.editorconfig` — `[dzil]` section: 4-space indent, LF, final newline, no trailing whitespace |
| Markdownlint | `npx markdownlint-cli --config .markdownlint.json .` | dash-style unordered lists, no line-length limit |
| Spellcheck | `pyspelling -c .spellcheck.yml` | pyspelling + aspell over `**/*.md` |

The `dzil` file has no extension; `.gitattributes` forces `linguist-language=Shell`
and `.editorconfig` targets it by literal `[dzil]` section name — keep the
filename as-is.

When spellcheck flags a legitimate term, add it to `.wordlist.txt` (one word per
line). `dictionary.dic` is a compiled aspell dictionary — do not hand-edit it.

## Contributions

Pull requests target the `master` branch (see `CONTRIBUTING.md`).
