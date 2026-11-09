# Cyiatic repository standard

How every public repository under [github.com/Cyiatic](https://github.com/Cyiatic)
is laid out, so a visitor can land on any of them and find the same things in
the same places.

Rules marked **must** apply to every repo. **Should** rules apply unless the
repo has a documented reason not to (put the reason in the README's
"Repository layout" section).

---

## 1. GitHub settings

| Setting | Rule |
| --- | --- |
| Name | **Must** match the project's display name (`CatchThat`, `TND6480i`). Lowercase-hyphen names are fine for tools/wrappers (`catastrophe-crow-standalone`). |
| Description | **Must** be one sentence, under 120 characters, saying what it *is* and what it's *for*. No trailing period. |
| Topics | **Should** have 3–6: one *kind* (`romhack`, `cli`, `website`, `electron`…), one *platform* (`n64`, `windows`, `discord`…), and one or two subjects. |
| Website | **Should** be set when the project has a live page, release page, or Neocities entry. |
| Default branch | **Should** be `main`. If another branch is the default (e.g. a distribution branch), the README must say why. |
| Releases | Tag as `vMAJOR.MINOR.PATCH`, or `vNN-short-name` for numbered ROM-patch candidates. Release notes live in `docs/releases/<tag>.md` and are pasted into the GitHub release. |
| Branches | Delete topic branches after they are merged. Long-lived non-default branches use a prefix: `fix/`, `experiments/`, `diagnostics/`, `candidates/`, `release/`. |

## 2. Files at the root

Keep the root short. Only these belong there:

| File | Rule |
| --- | --- |
| `README.md` | **Must.** Follows the template in section 3. |
| `LICENSE` | **Must.** Default is MIT for code. ROM-hack repos may use MIT for the scripts/docs and say clearly that it gives no rights to the game. |
| `.gitignore` | **Must** for anything with a build step, generated output, or local/private data. |
| `.gitattributes` | **Should** for repos with binary files or mixed line endings. |
| `CHANGELOG.md` | **Should** once the repo publishes releases. |
| `SECURITY.md` | **Must** for tools that touch personal data, credentials, or browser sessions. |
| `CONTRIBUTING.md` | Optional. |
| Tool files | `AGENTS.md`, `PRODUCT.md`, `DESIGN.md`, `package.json`, `pyproject.toml`, `Makefile`, and so on stay at the root when a tool needs them there. |
| Entry points | Only when users run them directly (`setup.bat`, `main.cjs`). |

Everything else goes into a folder: reports, dated notes, images, and one-off
scripts.

## 3. README template

Sections go in this order. Leave out any that don't apply, but never reorder
them. **Aim for under 200 lines.** Anything longer goes in `docs/` and gets a
link.

```markdown
<img src="assets/<repo>-logo.png" alt="<Project name>" width="483">

# <Project name>

<One or two sentences: what it is and who it's for.>

<Badges are optional. If you use them, keep it to one line: release, license.>

## Download / Install          ← for players and end users: the fastest path to using it
## Status                      ← what's tested and what isn't; current version/candidate
## Quick start                 ← for developers: the shortest working command sequence
## Documentation               ← table or list linking docs/; "I want to… → start here"
## Repository layout           ← only for repos with more than ~5 top-level folders
## Safety and privacy          ← for data and archive tools; "No ROMs" notice for ROM hacks
## Credits and provenance      ← original authors, base hacks, decomps, testers
## License                     ← one line, plus what the license does NOT cover
## AI Assistance Disclosure    ← always the final section (wording in section 6)
```

**Logo:**

- A wordmark or banner goes on its own line above the H1, at `width="483"` (the TND6480i / PD6480iperf size). Wrapping it in `<p align="center">` is fine.
- A square icon goes inline in the H1, at `width="64"`:

  ```html
  <h1><img src="assets/x-mark.png" alt="" width="64" align="absmiddle"> X</h1>
  ```

- Logos live in `assets/`, named `<repo-lowercase>-logo.<ext>`.

**Writing style:**

- Use second person and present tense.
- Write commands as fenced `powershell`, `bash`, or `text` blocks.
- Use relative links inside the repo.
- Put machine-specific values (IPs, usernames, VM paths) in as placeholders such as `<xp-host>`, never real ones.

## 4. Folder conventions

| Folder | Holds |
| --- | --- |
| `assets/` | README and branding images |
| `docs/` | Long-form documentation. Add a `docs/README.md` index once there are more than three docs. |
| `docs/releases/` | One file per release tag |
| `docs/archive/` | Dated handoffs, session notes, superseded status pages, and AI kickoff prompts. Keep them for history, out of the main docs list. |
| `src/` | Source code |
| `tests/` | Tests |
| `scripts/` | Developer and build scripts. Group subfolders by purpose (`hardware/`, `maintenance/`, `release/`). |
| `tools/` | Third-party or standalone helper tools (browser adapters, submodules) |
| `fixtures/` | Synthetic sample data only. Never real data. |
| `evidence/`, `reports/`, `diagnostics/` | ROM-hack validation output. One subfolder per candidate or version, each with a short `README.md`. |
| `private-data/`, `artifacts/roms/`, `output/`, `dist/` | Local-only. Git-ignored, keeping only a `.gitkeep` or `README.md`. |

**File names:**

- Lowercase kebab-case for new docs, e.g. `hardware-in-the-loop.md`.
- Upper case only for the conventional files (`README`, `LICENSE`, `CHANGELOG`, `SECURITY`, `INSTALL`, `BUILD`, `TESTING`).
- Put dates at the end as `-YYYYMMDD`.

## 5. Never commit

- Commercial ROMs, ISOs, SDK media, extracted game assets, or saves that aren't yours to share
- Credentials, tokens, `.env` files, exported PowerShell credential files, SSH keys
- Real chat captures or other personal data. Use `fixtures/` with synthetic data instead.
- Generated build output larger than a few MB. Publish it as a release asset instead.
- Machine-specific config, such as `.n64ez/config.json`

## 6. AI Assistance Disclosure (standard wording)

```markdown
## AI Assistance Disclosure

This project was developed with assistance from <tool(s)> for <areas, e.g.
reverse-engineering support, scripting, documentation>. The repository owner
directed the work, reviewed and tested the results, and remains responsible
for the project's technical claims and final decisions.
```

Optional add-ons, as one extra sentence each:

- **Hardware testing:** "Hardware setup, real-console testing, and subjective visual evaluation were performed by the repository owner."
- **Generated logos:** "The README logo was generated with AI from <reference>; it is a project identifier only and implies no affiliation with <rights holder>."

## 7. Commits

- Write the subject as a sentence in the imperative ("Add v88 release notes"), 72 characters or fewer, with no trailing period.
- Make one logical change per commit. Repo-wide clean-ups land as one commit titled "Apply Cyiatic repository standard".
- Credit an AI co-author with a `Co-Authored-By:` trailer.

## 8. Checklist for a new repo

- [ ] Description, topics, and website set
- [ ] `README.md` follows section 3, with a logo in `assets/`
- [ ] `LICENSE` present and named in the README
- [ ] `.gitignore` covers private, generated, and ROM files
- [ ] Docs over ~50 lines live in `docs/`, linked from the README
- [ ] AI Assistance Disclosure is the final README section
- [ ] No IPs, usernames, credentials, or ROMs in tracked files
