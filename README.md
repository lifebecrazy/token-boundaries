# Token Boundaries as Communication Cuts

**Research in progress — experiment snapshot: September 25, 2026.**

This project studies how token boundaries change the computation required by a
shallow Transformer, even when vocabulary size, sequence length, and token-length
histograms match. For a raw block `abc`, compare `[ab][c]` with `[a][bc]`: the
first makes the interaction between `a` and `b` token-local, while the second
makes the interaction between `b` and `c` token-local.

The working manuscript is titled *Token Boundaries as Communication Cuts: Exact
Raw-to-Token Accounting*. It studies distributed token-materialization costs,
matched boundary allocations, endpoint task reversal, and two-layer repair in a
specified causal finite-precision model. These are draft theoretical claims,
not general claims about arbitrary tokenizers or production language models.

## Current evidence

| Stage | Preserved and validated | What the count means |
|---|---:|---|
| Learning-rate pilot | 54 / 54 paired jobs | Tuning stage; not confirmation of the hypotheses |
| Coarse evaluation | 18 / 162 paired jobs | Incomplete; no full-grid performance conclusion |
| Refinement and allocation | Not started | Planned downstream stages |
| Independent human proof and novelty review | Pending | Automated checks do not close these reviews |

Each paired job trains two tokenizer conditions. The next nine-pair batch is
provided below, but its completion is not assumed. The project counts above are
recorded validation status; the corresponding historical result archives are
not included in this starter package.

An internal audit also identified an unresolved exact-constant question in the
cited one-layer communication simulation. The draft quotes the source theorem,
but the displayed proof arithmetic needs reconciliation before that numerical
constant is treated as independently checked.

## Run the next batch

1. Download [tokenization-coarse-colab.ipynb](tokenization-coarse-colab.ipynb).
2. Upload it to [Google Colab](https://colab.research.google.com/).
3. Select **Runtime → Change runtime type → T4 GPU**.
4. Keep `SHARD_INDEX = 2`, select **Run all**, and approve Drive access only if
   you want the optional backups.
5. Preserve the returned ZIP and summary for independent validation.

The notebook contains the frozen inputs and implementation. It runs **one
nine-pair batch**, not all 162 coarse pairs. It checks the T4/driver, input
checksums, locked environment, and bundled tests before training.

See [REPRODUCIBILITY.md](REPRODUCIBILITY.md) for requirements, file identities,
failure handling, and the distinction between collection and validation.

This September 26 presentation copy removes comments and explanatory docstrings
from the notebook's direct code cells. The five embedded experiment assets remain
unchanged, including their original source comments. Markdown run instructions
and runtime warnings are retained. An existing run does not need this new copy.

## Scope and limitations

- The exact chunk-cost statement assumes input-independent exact-substring chunks
  on a full binary product domain. Correlated inputs or compressive maps are outside
  that equality's scope.
- The width/depth statements concern the declared finite-precision model, with
  restrictions on attention heads, precision, and architecture. The learned-model
  hypotheses still require the prespecified evaluation.
- The BPE construction is restricted to a typed domain with engineered merge
  priorities; it is not a result for arbitrary learned BPE vocabularies.
- This package is not a completed empirical benchmark or a claim of conference
  acceptance. Independent human assessment of the mathematics and novelty remains
  necessary.

## Included files

- `README.md`: project overview and dated status.
- `REPRODUCIBILITY.md`: instructions and frozen checksums.
- `tokenization-coarse-colab.ipynb`: standalone next-batch notebook.
- `LICENSE`: full text of the CC BY 4.0 license.

No manuscript PDF, historical result archives, private run logs, account tokens,
or author metadata are deliberately added to this package.

## Credits and release status

The work builds on existing Transformer communication simulations, tokenizer
theory, split-output communication, and hypergraph cut functions. It does not
claim to originate those ingredients. The full manuscript bibliography should
accompany any eventual manuscript release.

This starter package does not yet assign authorship, a DOI, or a publication
venue.

## License

© 2026 Anonymous Authors. Released under the
[Creative Commons Attribution 4.0 International License (CC BY 4.0)](https://creativecommons.org/licenses/by/4.0/);
see [LICENSE](LICENSE) for the full text.
