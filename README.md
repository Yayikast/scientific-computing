# Scientific Computing (CSS322): selected coursework

Coursework from CSS322 Scientific Computing at SIIT, Thammasat University (2026, term 1).
Each project is a Jupyter notebook that runs top to bottom with fixed seeds, plus a short
written memo for a non-technical reader.

## Projects

### Week 3: Quantization and model compression (`week03-quantization/`)
Compared compressed versions of a small language model to decide which one to install on an 8 GB laptop.
- Implemented block-wise quantization on a 256 x 256 test layer with planted outliers and measured
  a cosine similarity of 0.99998 against the original output.
- Recommended q4_K_M: 397 MB instead of 994 MB and about 285 vs 186 tokens/s, while still passing
  3 of 4 behaviour tests. Rejected q2_K after it broke on arithmetic and language tests.

### Week 6: Sparse matrices and linear solvers (`week06-sparse-linear-systems/`)
Checked whether a review-similarity recommender and a city street-load model can run on one laptop.
- Showed that a dense 40,000 x 120,000 review matrix would need 38.4 GB and crash, while CSR sparse
  storage cut the test matrix from 384 MB to 2.33 MB (about 165x smaller).
- Built cosine-similarity search with sparse matrix-vector products (tens of times faster than dense).
- Wrote Jacobi and Gauss-Seidel solvers (71 and 39 sweeps) and compared them with `spsolve` and a dense
  solve, using residuals, `np.allclose` agreement and memory cost to choose the solver to ship.

### Week 9: Honest model evaluation (`week09-honest-evaluation/`)
Built a PM2.5 early-warning classifier for Bangkok schools and evaluated it without fooling myself.
- Time-ordered split, an "always safe" baseline (0.742) and a scaler + logistic regression pipeline (0.874).
- Reproduced two common leaks on purpose (shuffled split 0.918, a feature containing tomorrow 0.929)
  and repaired the second back to the honest 0.874.
- Chose the alarm cut-off from stated mistake costs on a validation set: 0.15 instead of 0.5,
  catching 44 of 47 dangerous test days instead of 33.
- Computed ROC-AUC two independent ways (trapezoid rule and pair counting), both 0.935.

## Skills
Python, NumPy, SciPy (sparse matrices, linear solvers), scikit-learn (Pipeline, TimeSeriesSplit,
ROC-AUC), reproducible notebooks, and writing results for non-technical readers.

## Run it
    python -m venv .venv
    .venv\Scripts\activate
    pip install -r requirements.txt

Then open any notebook and choose Restart & Run All.

AI use: I used Claude for explanations, debugging help and reviewing my work, as declared in each notebook.
