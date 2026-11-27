# Keeping up with upstream

Slideflow is a fork of [DeckCraft](https://github.com/storytold/deckcraft) (MIT or Apache-2.0).
This is how we take their updates without losing our name, icon and links.

## The one rule

**Every change Slideflow makes to a file that came from upstream is made by `rebrand/apply.py`,
never by hand.** The script reads `rebrand/brand.json` and can be run again at any time, so after a
merge we can take upstream's version of any conflicted file and re-apply our changes in one step.
`apply.py` is the same in every FlowApps fork; only `brand.json` differs.

## What lives where

| Ours (upstream has no such file, or we replace theirs whole) | Upstream's, changed only by `rebrand/apply.py` |
|---|---|
| `rebrand/` (`apply.py`, `brand.json`, `app-icon/`, `patches/`) | everything under `crates/`, `apps/`, `packaging/` |
| `brand/` (logos, `.ai` source) | `assets/app-icon/` (file names theirs, artwork ours, from `rebrand/app-icon/`) |
| `docs/UPSTREAM.md`, `README.md`, `assets/header-*.png` | `CLAUDE.md`, `NOTICE`, `.gitattributes`, `.gitignore` |
| `.github/workflows/release.yml`, `windows-release.yml` | |

`brand.json` holds:

- **edits**: find and replace in one file (window title, bundle id `com.slideflow.app`, version
  and log lines, Mac `Info.plist.in` and `package.sh`, Windows installer names and links). Every
  occurrence is replaced; `"regex": true` uses a regular expression.
- **prepend / append**: text added once (the agent note in `CLAUDE.md`, our `NOTICE` paragraph,
  merge rules in `.gitattributes`, release-build lines in `.gitignore`).
- Patches in `rebrand/patches/` for changes too big for find and replace, applied with a
  three-way merge: no Discord or ArtCraft links in the About box, backstage screens, CLI or AI-agent server.
- Icons: `rebrand/app-icon/` copied over upstream's files of the same names.

Left alone on purpose: crate and binary names (`deckcraft*`), environment variables, log-file names,
licences and credits, upstream's docs, Linux packaging (we don't ship Linux), and the Windows
installer ids and `deckcraft.exe` (changing them would stop installed copies from upgrading). The
settings folder stays `Slideflow`, because existing users' settings live there.

## Which upstream version we follow

DeckCraft cuts releases on side branches, so their release tags are not on `main`. Slideflow follows
their `main`.

## Merging upstream

Set the clone up once, so upstream's tags arrive as `upstream/v…` and never collide with ours:

```bash
git remote add upstream https://github.com/storytold/deckcraft.git
git config remote.upstream.tagOpt --no-tags
git config --add remote.upstream.fetch '+refs/tags/*:refs/tags/upstream/*'
git config merge.ours.driver true
```

Never push the `upstream/*` tags. Then:

```bash
git fetch upstream
git checkout -b upstream-sync
git merge upstream/main
```

If there are conflicts:

1. For a file in the right-hand column above, take theirs: `git checkout --theirs -- <file>`.
2. For a file we deleted that they changed ("deleted by us"): keep it deleted, `git rm <file>`.
3. For `README.md` or our workflows, keep ours: `git checkout --ours -- <file>`.

Then re-apply the rebrand and check it:

```bash
python3 rebrand/apply.py
python3 rebrand/apply.py --check     # prints nothing and exits 0 when everything is rebranded
```

If the script stops with `could not find … to edit`, upstream changed that line: find where the
text went and update that entry in `rebrand/brand.json`. If a patch leaves conflict markers,
resolve them, then refresh the patch with
`git diff <upstream commit> -- <its files> > rebrand/patches/01-no-discord.patch`.

Build and test, commit and open a pull request:

```bash
cargo build --locked -p deckcraft
cargo test --locked --workspace --no-fail-fast
```

Run the app once and look at it before releasing: tests don't see icons or the title bar.

### Known work for the next merge

Tried on 2026-11-26 against upstream `main` (74591aba, 49 commits ahead): `brand.json` stops at
`apps/deckcraft/src/main.rs`, because upstream moved the app's identity out of it:

- The settings folder moved to `apps/deckcraft/src/app_dirs.rs`, and its tests assert the names.
- `profile_root.rs` has `p.join("DeckCraft")`.
- Window title, app id and name come from `deckcraft_ui_egui::os_window` (`LaunchIdentity`,
  `id_for`, `name_for`, Stable and Nightly), so those edits move to
  `crates/ui-egui/src/os_window.rs`, as in Wordflow.

## Releasing

Actions → Release builds the macOS DMG and the Windows portable zip and publishes a GitHub
release. The FlowApps launcher installs and updates Slideflow from those releases.
