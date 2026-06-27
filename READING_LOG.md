# Reading Log

A running log of what I read, why, and what I took from it. The entries are ordered roughly by when I encountered them, not by importance.

For each paper:
- **Status** — `to-read` / `reading` / `read`
- **Why this paper** — its role in the lit review (foundational, closest prior work, contrarian, methods, etc.)
- **Take-home (one paragraph)** — what I'd tell someone in plain words
- **Bearing on my question** — how it informs the design

---

## 1. Huh et al. (2024) — *Position: The Platonic Representation Hypothesis*

- **Venue:** ICML 2024 (Position paper)
- **arXiv:** [2405.07987](https://arxiv.org/abs/2405.07987)
- **Role:** Foundational. Names the central conjecture this whole project sits against.
- **Status:** to-read

### Why this paper

This is the paper that crystallized the idea that representations across different models, architectures, and modalities are converging to a shared statistical structure as models scale. Everything in cross-model representation work for the past two years cites it. Read this first — every other paper in this log refers back to it.

### What I expect to find

A position-paper argument (not a single empirical result) marshalling many findings from the prior literature to argue for convergence. Likely uses mutual-nearest-neighbor and CKA-style metrics to demonstrate alignment.

### Take-home (fill after reading)

_TBD._

### Bearing on my question

_TBD. Things to look for: what metrics they use to claim convergence, whether they distinguish global vs local structure, what they say about correspondence without shared-input anchoring._

---

## 2. Jha, Zhang, Shmatikov, Morris (2025) — *Harnessing the Universal Geometry of Embeddings*

- **Venue:** Preprint (under review as of mid-2025; cited as Cornell CS)
- **arXiv:** [2505.12540](https://arxiv.org/abs/2505.12540)
- **Role:** Closest prior work to my question. **Read carefully — the contribution of my paper must be the part this one did not cover.**
- **Status:** to-read

### Why this paper

This is the most direct prior work on cross-model embedding correspondence. They introduce `vec2vec`, an unsupervised method that translates text embeddings between vector spaces *without any paired data*. They report cosine similarity as high as 0.92 to ground-truth target vectors, and perfect matching on 8,000+ shuffled embeddings. They explicitly frame the result as supporting a "Strong Platonic Representation Hypothesis." Preliminary CLIP experiments suggest the method extends to other modalities.

### What I expect to find

A method (adversarial losses, cycle consistency, vector-space preservation) for learning a mapping between two embedding spaces using only unpaired samples. Strong reported results on text-text translation; preliminary multimodal results. Likely scoped to specific encoder pairs and specific datasets.

### Take-home (fill after reading)

_TBD._

### Bearing on my question

**This is the critical one to scope against.** Things to look for:

- Exactly which model pairs were tested (text encoders, CLIP) — what's *not* covered?
- Whether they characterize *when* the method works vs. fails (or just demonstrate that it works on chosen pairs)
- Whether they test transitivity / chaining across multiple model pairs
- Whether they connect recovery success to geometric properties (intrinsic dimensionality, isotropy, etc.) — this is where my contribution likely lives
- Whether the method requires training a translator (their approach) or whether simpler structure-only matching also works (potentially my contribution)

The honest read: vec2vec is evidence that recovery *is possible*. My paper is likely about characterizing *when, why, and how well* — not about whether it's possible at all.

---

## 3. *Revisiting the Platonic Representation Hypothesis: An Aristotelian View* (2026)

- **Venue:** Preprint (Feb 2026)
- **arXiv:** [2602.14486](https://arxiv.org/abs/2602.14486)
- **Role:** Critical / contrarian view. The empirical pushback on PRH.
- **Status:** to-read

### Why this paper

This is the most recent and most relevant *critical* response to PRH. It argues the observed convergence may be an artifact of model width/depth (a confound) rather than evidence of genuine shared structure. It also flags concerns about the metrics PRH relies on — that mutual-nearest-neighbor alignment "measures similarity, not sameness." Both of these critiques bear directly on the design of any follow-up.

### What I expect to find

An empirical paper that controls for model width and depth and shows that some of the apparent convergence disappears when those are held fixed. Likely also a metric-comparison section showing that different similarity measures give different answers.

### Take-home (fill after reading)

_TBD._

### Bearing on my question

This paper is the strongest argument for why my question matters — if convergence is partly a metric/scale artifact, then asking whether correspondence is recoverable from geometry *without shared-input anchoring* is a sharper test of whether the structure is real.

Things to look for:
- What confounds they identified, and whether my proposed experiment controls for them
- Whether they propose alternative metrics, and whether those could be used in correspondence recovery
- What they don't address — the gap to my contribution

---

## Further reading (queued)

The next ~7 papers to source, to round out to the planned 10. Suggested directions (to refine):

- **Intrinsic dimensionality work** — Ansuini, Gong (already cited in HNSW paper); recent work on retrieval embeddings having higher ID than classification embeddings.
- **Local vs global geometry** — recent papers showing k-NN-based local metrics catch things CKA/RSA miss.
- **CKA and related metrics** — Kornblith et al. 2019 (CKA), the metric-comparison literature.
- **Unsupervised word embedding alignment** — Conneau et al. (MUSE), Grave et al. — the inspiration vec2vec drew from.
- **Cross-modal alignment** — CLIP paper (Radford et al. 2021), since multimodal correspondence is rung 2 of the design.

To be sourced together later. Today's task: get the first 3 above into reading flow.
