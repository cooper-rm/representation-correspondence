# Research Question

## The question, in plain terms

**If I have a point in one model's embedding space and a point in another model's embedding space, how do I tell whether they mean the same thing?**

## Two faces of the same question

This single question has two interleaved aspects, and the paper answers both:

### The definition aspect

What does it *mean* for two points from two different embedding spaces to be "the same"? The trivial answer is "they came from the same input," but that depends on shared-input anchoring. Without that anchoring, "same" needs an operational definition — and proposing a good one is itself a contribution.

### The detection aspect

Given two embedding spaces, *can* we recover which point matches which, using only geometry? This is the runnable, experimental version. The answer is a number: correspondence-recovery rate.

The detection aspect operationalizes the definition aspect: points correspond if the local geometry around them matches well enough that a structure-only matcher pairs them.

## Hypothesis

Cross-model embedding correspondence is at least partially recoverable from local geometric structure — k-nearest-neighbor overlap, relational distance, local intrinsic dimensionality. The hypothesis is testable, and the experiment must be designed so it could come out false.

## Three rungs

The work escalates in difficulty:

1. **Same modality.** Two image models (e.g., CLIP-ViT vs DINOv2) on the same images. Embed, hide the correspondence, recover from geometry. Establishes the method works at all.

2. **Cross modality.** An image model vs a text model. Does an image of a cat correspond to the word "cat" via geometry alone? Stress-tests the hypothesis across modality boundaries.

3. **Transitivity.** If image↔image and image↔text both work, does the composition chain? Is `image → (via image-model-B) → text` consistent with the direct `image → text` correspondence? **This rung is the deepest test of whether there is one shared underlying structure or several independent pairwise alignments.**

## Honest constraints on the design

- **Transitivity is a hypothesis to test, not a goal to confirm.** The experiment must be able to come out negative. "It succeeds (or fails) because of transitivity" only counts as a finding if transitivity is operationalized as a *specific testable prediction* — e.g., composed correspondences match direct correspondences within some error bound.

- **Watch for alternative explanations.** If cross-model correspondence succeeds, transitivity is one explanation among several. Could also be: shared training data, shared cluster structure, matcher exploiting shallow features. A good paper rules these out before claiming transitivity.

- **Recovery may be only partial.** "Geometry alone recovers ~40% of correspondences" is a publishable finding. "Geometry alone fails for cross-modal" is *also* a publishable finding, possibly more interesting.

## What needs to be locked before deep work

- [ ] Model pairs (which encoders, same modality + cross modality)
- [ ] Input set (size, diversity, source — must be runnable on available compute)
- [ ] Matching method (what geometry-only matcher; nearest prior work uses adversarial methods, simpler options exist)
- [ ] Primary metric (correspondence-recovery rate at top-k? cosine similarity to ground-truth match?)
- [ ] Venue target (shapes scope and length)
- [ ] Cadence with advisor (Busch)

## Nearest prior work to read closely

See `READING_LOG.md`. The closest is Jha et al. 2025 (*Harnessing the Universal Geometry of Embeddings*, vec2vec) — read this carefully before designing experiments, so the contribution here is the part it did not cover.
