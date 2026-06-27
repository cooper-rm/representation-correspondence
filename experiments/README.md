# experiments/

Runnable experiments. Each experiment lives in its own subdirectory with:

- A `README.md` stating the question, hypothesis, and expected output
- The code to run it
- A `requirements.txt` if it has dependencies beyond the project default
- `output/` for results (gitignored)

## Planned experiments

- `01_same_modality_recovery/` — two image models on the same image set; recover correspondence from local k-NN structure alone
- `02_cross_modality_recovery/` — an image model and a text model on paired data; same recovery task
- `03_transitivity/` — chain image-to-image with image-to-text; check whether the composition matches direct image-to-text

None of these are designed yet. Lock the scope (model pairs, input set, metric) before writing any code — see `RESEARCH_QUESTION.md`.
