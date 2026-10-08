# Split audit — K5-ocean-probes

How this repository was carved out of the pristine **K** monorepo. Regenerate the classification with `python3 K-audit/classify.py K5-ocean-probes` and re-check the import graph with `python3 K-audit/verify_repo.py K5-ocean-probes`.

## Claim cluster

ice–ocean double diffusion (salt + temperature).

Source: `ocean/**` + `scallop_probe.py` + `subglacial/{__init__,candidate2_doublediff,candidate3_roughness_feedback}.py` (the double-diffusion solvers the ocean runners import).

## Composition

| | files |
|---|---|
| traced to a monorepo file | 17 |
| byte-identical copies | 14 |
| modified (see *Edits*) | 3 |
| new (not in the monorepo) | 1 |

Source directories, by file count:

- `ocean/` — 4
- `ocean/figures/` — 4
- `(monorepo root)`/ — 3
- `glaciers/subglacial/` — 3
- `ocean/tests/` — 2
- …plus 1 file(s) that sit alone in their source directory (top-level scripts, one-off reports)

## Vendored files

Copied byte-for-byte from the monorepo paths below (this is what makes the repo import-clean on its own):

- `REPORT_CANDIDATE2.md`
- `REPORT_DOUBLEDIFF.md`
- `run_candidate2.py`
- `scallop_doublediff.py`
- `scallop_probe.py`
- `figures/48_candidate2_doublediff.json`
- `figures/48_candidate2_doublediff.png`
- `figures/50_scallop_doublediff.json`
- `figures/50_scallop_doublediff.png`
- `subglacial/__init__.py`
- `subglacial/candidate2_doublediff.py`
- `subglacial/candidate3_roughness_feedback.py`
- `tests/test_candidate2.py`
- `tests/test_doublediff_scallop.py`

## Edits

- `README.md` — rewritten for standalone use (see below).
- `README.md` — rewritten to stand alone: no `../` links into sibling monorepo folders, run commands given from the repo root, and a Provenance section pointing at the archive.
- `pyproject.toml` — rewritten for this repo: `testpaths`/`pythonpath` scoped to this repo instead of all five monorepo domains, and the dependency list trimmed to the libraries this claim cluster imports.
- `requirements.txt` — rewritten for this repo: `testpaths`/`pythonpath` scoped to this repo instead of all five monorepo domains, and the dependency list trimmed to the libraries this claim cluster imports.

## Excluded files

- none: every monorepo file belonging to this claim cluster was carried over.

## Test-suite accounting

`tests/` carries **2 test files** (ocean/tests (2)); the whole monorepo has 136 test files across the five repos (78+36+15+2+2 = 133, plus the 3 excluded in K1).

## Verification

`K-audit/verify_repo.py` walks the **AST import graph** of every Python file in this repo, expands each unqualified import against every `sys.path` root the file would actually see, and reports any import that resolves only outside the repository. Result:

```
OK K5-ocean-probes: no external edges
```

## Provenance

Pristine snapshot taken **before** any edit: `K-monorepo-archive.tar.gz` (SHA-256 `3c30c68b4d4287787af00539b2cbe75a47dc0536491ec0d1b17a0f61d80b5304`). `FUTURE_WORK.md` / `PAPER_OUTLINE.md` were deliberately left in the archive.
