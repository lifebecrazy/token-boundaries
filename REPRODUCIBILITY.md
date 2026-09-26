# Reproduction guide

## What this package runs

The notebook reproduces one shard of the frozen theorem-faithful coarse registry.
The default is zero-based shard **2 of 18**, containing nine `ab_intersection`
depth-1, seed-3 paired jobs: `n = 16, 64, 128` crossed with widths `8, 32, 128`.
Each pair uses the registered settings, including 2,000 steps and batch size 256.
Do not interpret this shard alone as the complete evaluation.

The notebook embeds five unchanged files:

| File in the notebook | SHA-256 |
|---|---|
| `tokenization-pilot-bundle.zip` | `85c44af07f6e75537b96b9b1befae4b4b584e7ba8d9a2732e290d88ef8bc7efd` |
| `tokenization-coarse-manifest.json` | `cffeeacb1bbc23def9f035cc4f6a3a4578112b259a0d0703d86fa2b93f333429` |
| `tokenization-coarse-learning-rates.json` | `05dd63a4b52015e6b89e267c22355d848a4cde8741277b81915a15393b25ca7d` |
| `colab-cli-coarse.py` | `43106d96673d2b76b3a66d041c8b2618a753bce38372594862b1196067747b59` |
| `colab-cli-coarse-collect.py` | `7b14309d67819733a7c4171167c25a48a80927528e1a60d8874f3ec668adc456` |

The release bundle's historical filename contains `pilot`; the supplied notebook
uses the separately frozen **coarse** manifest and selected learning rates.

The September 26 presentation copy removes comments and explanatory docstrings
from the ten direct notebook code cells. It retains Markdown instructions, runtime
warnings, settings, and all five embedded assets byte-for-byte. Comments inside
the embedded experiment sources are therefore still present. This cleanup does
not change the experiment implementation or establish human authorship.

Delivered notebook: **8,296,565 bytes**. SHA-256:
`bef987c4c08537e07879aa000a5c79057e8ef20c84901f59c178d8bf3f214fb6`.
Colab may change notebook metadata when saving a copy; the embedded-input hashes
are checked independently at execution time.

## Environment

Use a fresh Colab T4 runtime. The notebook selects Python 3.12 through `uv`, installs
`uv==0.9.29`, and uses the bundled lockfile rather than Colab's preinstalled PyTorch.
The frozen environment includes NumPy 2.5.2, PyTorch 2.13.0, pytest 9.1.1, and Ruff
0.16.2. The Linux PyTorch build uses CUDA 13. The notebook requires driver branch
580 or newer and does not provision forward-compatibility packages.
See [NVIDIA's compatibility table](https://docs.nvidia.com/deploy/cuda-compatibility/minor-version-compatibility.html).

Package installation needs internet access and can take several minutes. A T4,
runtime duration, and successful dependency downloads are not guaranteed.
Do not silently substitute package versions or another GPU when a check fails.

## Save the evidence

Drive backups are optional. Mounting Drive grants notebook code access to that
Drive; backups go to a new folder under `MyDrive/tokenization-results`.
Completed-pair snapshots are labelled `UNVALIDATED`. A failed copy prints
`BACKUP FAILED` and does not stop local training or final collection. An incomplete
Drive file is preserved rather than overwritten automatically.

After success, the collector packages the progress ledger, launch identity,
execution log, nine result JSONs, eighteen checkpoints, and hardware record.
The final ZIP has 31 members. Save the accompanying summary, which records the
archive checksum and frozen manifest identities.

Collection checks completion and provenance; it does **not** replace independent
scientific result validation and import. Before increasing the project's validated
count, validate every returned result and checkpoint against its registered job.
Do not publish accuracy claims from a partial grid.

## Interrupted runs

- Do not rerun the launch cell over an existing run directory.
- If only the monitor cell was interrupted, keep the same kernel and rerun that cell.
- The frozen collector requires the original process handle and a complete fresh
  shard. Automatic resume after a lost runtime or kernel reset is not supported.
- If the runtime is lost, this notebook requires a fresh run of the shard. Preserve
  any partial snapshots separately; do not discard them or count the new run twice.
- Partial snapshots preserve evidence but are not drop-in final archives.
- If browser download fails, rerun only the last download cell. If Drive failed,
  download the local ZIP and summary before the runtime disappears.

The notebook does not evade Colab session limits. Consult the
[Colab FAQ](https://research.google.com/colaboratory/faq.html) for runtime persistence.

## Checks performed before this handoff

On September 25, 2026, the development workspace passed 1,311 tests, including 16
new notebook-specific tests. Ruff, notebook-schema validation, compilation of all
10 executable cells, deterministic notebook reproduction, and code review passed.
All five frozen inputs and all 17 scientific Python modules retained their hashes.

On September 26, the presentation-copy check passed 1,319 tests, including eight
new cleanup tests. Four expected duplicate-ZIP warnings came from negative test
fixtures. Ruff, notebook-schema validation, code-cell compilation, and independent
code review passed. Direct-cell checks found zero comments or docstrings; all
embedded bytes, Markdown instructions, and scientific-module hashes were preserved.
The cleanup tests also exercised launch and collection with a real local process.

That is a **local software-verification report**, not a new GPU result or a proof
of the mathematics. The full development test suite is not separately distributed
here; the notebook runs the checks supplied by its frozen release bundle.
