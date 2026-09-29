# AGENTS.md — layer-kde-shell

Standalone candy repo for the `kde-shell` layer — the SDDM-free KDE Plasma
Wayland session package leaf shared by the bare-metal KDE desktop and the
headless streamed KDE pod. The candy lives in `charly.yml` at the repo root: the
`pod-dbus` require, the `distro:` package/AUR sections, the `check:` assertions,
and the embedded `skill:` entity projected into the marketplace corpus as
`/charly-selkies:kde-shell`.

Canonical files:

- `charly.yml` — the `kde-shell:` candy entity and the `kde-shell-skill:` skill
  entity.
- `.github/workflows/tag-on-merge.yml` — CalVer tag + `CHANGELOG/` on merge.
- `README.md` — user overview only; never agent guidance.

## Load these skills first (R0)

- `/charly-selkies:kde-shell` — the owning skill. The package partition (what
  lives in `kde-shell` vs `kde-desktop`), the `kdotool` AUR entry, and the two
  consumers. Load before editing or troubleshooting the layer.
- `/charly-image:layer` — the candy authoring reference (`charly.yml` schema,
  `plan:` step verbs incl. `check:`, per-distro `distro:` arms incl. `aur:`,
  package sections). Load before editing any entity field or plan step.

## Build / validate / test

- The merge gate is the **org-wide** `charly/pr-validator` (required check
  `validate / validate`, defined in `opencharly/.github`); this repo has **no
  per-repo candy gate** and ships only `.github/workflows/tag-on-merge.yml`.
- The candy's `plan:` `check:` steps are the functional evidence; they must stay
  valid on every distro arm they run on. Scope a distro-specific check in the
  command itself — the check runner does not honour runner-level
  `exclude-distro` fields.

## Modify this repo

- Edit the `kde-shell:` candy entity AND the `kde-shell-skill:` skill entity in
  `charly.yml` together. The skill is the projected usage source, so a behaviour
  change not mirrored in the skill leaves the corpus stale.
- This is a shared package leaf: workstation-only extras belong in the
  `kde-desktop` consumer, not here, so the streaming pod is not bloated. Keep
  the partition boundary and the `check:` binary paths in sync.
- New behaviour claims belong in the `plan:` as an observable `check:` step, and
  in the skill body.

## Landing

- PR-only. Every change lands through a pull request; the org-required
  `charly/pr-validator` validates the diff and body and arms native auto-merge
  on PASS. Direct pushes to `main` are blocked.
- History lives in `CHANGELOG/` (written by `tag-on-merge` at merge time); the
  PR body IS the changelog.
- The authoritative rulebook is the umbrella `AGENTS.md` in
  `opencharly/opencharly` and `charly/AGENTS.md` in the charly repo. Do not
  restate its rules here.
