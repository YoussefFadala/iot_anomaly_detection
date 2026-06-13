# Experiment Log
_Youssef Fadala — IoT Anomaly Detection FMP_

---

## Section 1: Project Milestones & Data Decisions

| ID   | Date       | Phase       | Outcome                                                                 |
|------|------------|-------------|-------------------------------------------------------------------------|
| M001 | 2026-06-08 | Setup       | Repository initialised, folder structure created, pushed to GitHub      |
| M002 | 2026-06-09 | EDA         | Full IoT-23 small dataset explored — 325,309,946 rows, 23/23 files loaded via chunked reading (chunksize=5,000) |
| M002 | 2026-06-09 | EDA         | Class imbalance confirmed: Benign 30,860,691 (9.5%) vs Malicious 294,449,255 (90.5%) — ratio 1:9 |
| M003 | 2026-06-09 | EDA         | Attack types identified: PortScan 65.7%, Okiru 18.7%, DDoS 6.0%, C&C <1% |
| M004 | 2026-06-09 | EDA         | Label inconsistency found: 'Benign' vs 'benign' — fix: .str.lower().str.strip() in preprocessing |
| M005 | 2026-06-09 | EDA         | Columns flagged for removal: local_orig, local_resp (all dashes), uid, id.orig_h, id.resp_h (non-generalisable) |
| M006 | 2026-06-09 | EDA         | Risk 2 materialised: 13/23 files exceed RAM. Mitigation: chunked reading applied successfully |
| M007 | 2026-06-09 | Decision    | VAE de-scoped — acknowledged in dissertation as future work             |
| M008 | 2026-06-09 | Decision    | Sampling strategy TBD — to confirm with supervisor: scenario-based subset |

---

## Section 2: Model Experiment Log

> _This section will be populated from Week 4 onwards when model training begins.
> _Threshold for all models set once on validation set and frozen — never re-tuned on test set.

| ID   | Date | Model | Dataset Subset | Feature Count | Key Hyperparams | AUPRC | F1 | FPR/hr | Latency (ms) | Notes |
|------|------|-------|----------------|---------------|-----------------|-------|----|--------|--------------|-------|
| E001 | —    | Isolation Forest  | —  | — | n_estimators=100, contamination=? | — | — | — | — | Pending Week 4 |
| E002 | —    | One-Class SVM     | —  | — | kernel=rbf, gamma=?               | — | — | — | — | Pending Week 4 |
| E003 | —    | Autoencoder       | —  | — | bottleneck=8, loss=Huber          | — | — | — | — | Pending Week 5 |
| E004 | —    | Deep SAD          | —  | — | eta=?, label_ratio=5%             | — | — | — | — | Pending Week 6 |

---

## Section 3: Ablation Study Plan

> _To be completed during evaluation (Week 7)._

| Ablation | Variable | Values to test | Purpose |
|----------|----------|---------------|---------|
| A001 | Deep SAD labelled-set size | 1%, 5%, 10% of attack labels | How much does label budget affect AUPRC? |
| A002 | Anomaly threshold (Autoencoder) | mean + 1σ, 2σ, 3σ | Sensitivity of F1 and FPR to threshold choice |
| A003 | Feature set | Full vs without IoT-specific features | Do derived features add value? |
| A004 | IF on raw features vs AE bottleneck | Raw vs latent representation | Does AE learn useful representations? |