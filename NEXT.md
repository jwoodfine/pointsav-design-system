# NEXT.md — pointsav-design-system

> **Scope: this repo only.** Cross-repo and workspace-level open
> items live at `~/Foundry/NEXT.md`.
>
> Read at session start when a Root Claude opens in this repo. Update
> at session end when repo-scope open items change.

Last updated: 2026-04-22.

---

## Currently open

- **Confirm bilingual README compliance at repo root.** Per the
  2026-04-22 audit, `README.md` is present; verify `README.es.md` is
  current and correctly paired. Repo carries design-system assets
  and tokens that downstream repos depend on — bilingual documentation
  matters.
- **Consider per-sub-asset documentation.** The `tokens/`, `assets/`,
  `components/`, `themes/`, and `templates/` subdirectories are the
  design-system's working areas. They do not yet carry their own
  `CLAUDE.md` / `NEXT.md`. Decide whether they need them — this repo
  is a single coherent artefact per the framework, so the answer may
  be "no," but worth settling explicitly.

## Recently closed (2026-04-22)

- Audit cleanup — 7 tracked `.DS_Store` files removed across
  `assets/`, `tokens/`, and their subdirectories. `.gitignore`
  created with `.DS_Store` entry. Commit `015d074`.

## Pointers

- Workspace-level open items: `~/Foundry/NEXT.md`
- Workspace changelog: `~/Foundry/CHANGELOG.md`
- Repo-level `CLAUDE.md`: `CLAUDE.md` (repo-level rules; first
  per-repo `CLAUDE.md` in the Foundry flow, added 2026-04-21).
