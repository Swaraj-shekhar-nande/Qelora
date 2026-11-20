# Qelora — static product website and reproducible positioning model

Working product identity for the proposed photon-timing / QKD positioning platform. Prepared 20 November 2026. No company registration, trademark clearance, certified security or measured field performance is implied.

## Publish the repaired website on GitHub Pages

The previous deployment served HTML but returned HTTP 404 for `assets/styles.css`. That produces the plain text, missing logo and oversized diagram shown in the reported screenshots.

This release embeds CSS, images, page JavaScript, saved results and the simulation worker into each HTML page. The layout and interactive model no longer depend on a separately uploaded `assets` or `data` folder. Links between pages and downloadable ZIPs remain relative, so the same release works beneath `/Qelora/`.

1. Extract this ZIP completely.
2. Upload **all extracted contents** into the folder GitHub Pages publishes. Replace the old HTML files. Do not upload only the ZIP itself or add an extra enclosing folder.
3. Keep `index.html`, `explorer.html`, `example.html`, `technology.html`, `theory.html`, `evidence.html` and `privacy.html` together. Keep `downloads/` for the downloadable research files; keep `.nojekyll` too.
4. In repository Settings > Pages, select Deploy from a branch, then the correct branch and folder, normally `main` and `/ (root)`. If your existing site uses `/docs`, update that folder instead.
5. Wait for the deployment to finish, then open the Pages address and press Ctrl+F5. Check the headline, logo, explorer and evidence page.

GitHub's browser uploader may flatten files when files from different folders are selected together. Drag the extracted folders with their contents, upload folders in the correct location, or use Git. The embedded pages remain styled even if the optional `assets/` folder is omitted; download links still require `downloads/`.

This package repairs the uploaded website. It does not update a GitHub repository until its extracted contents are published there. No build command, npm install, backend, database or API key is required for deployment.

## Open locally

You can open `index.html` directly to view the self-contained pages. For a consistent test of all pages, the simulation worker and file downloads, serve the extracted folder with `python -m http.server 8000` and open `http://localhost:8000/`. Use a current Chrome, Firefox, Edge or Safari browser. External research links require internet access.

## Opening-page security statement

The headline is **Secure timing. Precise positioning.** The surrounding text identifies this as a research concept, with BBM92 key establishment, initially authenticated classical communication, distinct per-anchor report authentication, freshness checks and monitored timing/calibration health. It does not claim that quantum keys alone prevent asymmetric optical delays, radio relays or compromised endpoints. The system-design page explains each protection and its assumptions, with primary references.

## Verification for this repair

All embedded scripts passed syntax checks. The supplied numerical regression suite passed without changing `model.js`. Browser checks confirmed styled rendering, working navigation and presets, a 500-trial Monte Carlo run with zero solver failures, ten populated evidence rows and no broken embedded figures. Homepage and explorer were checked at a 390-pixel frame width, including the mobile navigation. Standalone pages were also tested beneath a subdirectory with the `assets/` and `data/` folders absent.

## Pages

- `index.html`: product story, original logo, proposed founding team and timing / trust boundary.
- `explorer.html`: draggable UE, clock / signal / geometry controls, projected variance, clock sweep, nonlinear Monte Carlo in a worker, ensemble and fixed-installation modes, JSON export.
- `example.html`: complete calculation for UE (4,3) km with link ranges, TDoAs, timing budget and offline trial checks.
- `theory.html`: step-by-step observation, correlation and estimation equations with primary references.
- `technology.html`: architecture, ingredients, uplink / downlink choice, radio timestamping and workflow diagrams.
- `evidence.html`: corrected shared-scale maps, validation, sensitivity, bias and downloadable source / figures.
- `privacy.html`: local calculation and model status.
- `404.html`: static fallback.

## What was corrected

Under equal independent receiver errors, changing a scalar timing variance scales the entire geometry map. Independently normalized colour bars hide that scale change. Identical shapes are not, on their own, evidence of a bad calculation. The revised comparison shares one absolute scale and reports improvement explicitly. It also declares distance-dependent pilot energy and correlated refractivity errors.

The current example predicts 9.76 cm RMS and the saved Monte Carlo campaign gives 9.74 cm RMS, using an explicit budget; do not describe its difference from any earlier budget as a hardware improvement.

## Numerical model and checks

Clock input means **pairwise RMS**, hence independent per-BS RMS = input / sqrt(2). Known UE height 1.5 m, BS height 30 m, four available radio links. The reference signal is an ideal flat 100 MHz spectrum with usable pilot E/N0 = 20 dB at 10 km, free-space distance scaling, extra 100 ps receiver jitter, 100 ps RF calibration residual, 50 ps independent path residual, 1 cm survey uncertainty per coordinate and 1 N-unit common residual refractivity. Mean propagation delay is assumed corrected. Noise and clock errors are Gaussian under the nominal model.

The solver jointly fits x, y and unknown emission distance using full covariance. Coarse initialization is based on noisy observations (9×9 in Python, 7×7 in the browser); truth initialization and boundary clipping are not used. The Python grid has 31×31 positions ×800 trials ×2 clock settings = 1,537,600 nonlinear fits. Ten selected checks use 12,000 trials each. An independent SciPy solver agrees within 10 micrometres for 48 noisy test cases.

The live heatmap and sweep are local covariance predictions, not Monte Carlo maps. The browser trial button runs actual nonlinear timestamp fits. Browser and Python use different random streams, so samples are not identical. Slowly varying offsets stay fixed within the “One fixed installation” run. A +3 ns BS3 delay is unmodeled by the estimator; no zero-mean Gaussian R95 is advertised for that case.

The estimator uses known nominal link statistics at the selected scenario point. A field system must infer or calibrate them. This is a timestamp-level model, not a waveform, terrain, RF-coverage, optical-clock-servo or security simulation. Numerical convergence does not imply usable radio coverage. Four timestamps with three fitted states leave one residual degree of freedom, so a residual gate cannot guarantee rejection of bad delays.

## Reproduce

Download or unzip `downloads/simulation-source.zip`. Install Python 3 with numpy, scipy and matplotlib, then run `python simulate.py` from that folder. This repeats the full grid campaign and regenerates figures and data. Runtime depends on the machine. All seeds and checks are included. `downloads/figures.zip` includes editable SVGs and high-resolution PNGs.

For the browser numerical regression checks, use the separate developer source supplied in `downloads/website-development.zip`: run `npm test` or `node tests/model.test.mjs`. No npm packages are needed. The checks cover Python/JS covariance and radial R95 agreement, correct pairwise conversion, correlated-reference TDoA equivalence, common-mode invariance, noiseless boundary recovery, clock monotonicity, nonlinear Monte Carlo agreement, deterministic seeds and the bias/scatter identity.

## Editing

The published HTML is self-contained. Editing `assets/styles.css` alone does not change its embedded styles. For reproducible edits, extract `downloads/website-development.zip`, edit `qelora-source/` and run `python tools/build_standalone.py`. This rebuilds `qelora-fixed/`. Shared colors and layout are in the source `assets/styles.css`; math is in `assets/model.js`; explorer behavior in `assets/explorer.js`. If you change the model, regenerate reference data and plots before claiming numerical agreement. The generated symbol is in `assets/qelora-mark.png`; the wordmark is styled HTML. The logo is a working design concept and has not been trademark-cleared.

No tracking or external fonts are embedded. External research sources keep their own rights; linked papers are not redistributed. Website source and diagrams were created for this project.
