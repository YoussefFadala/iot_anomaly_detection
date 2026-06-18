# Report Structure Guide — PLANNING SCAFFOLD (not report text)

> ⚠️ This maps WHERE things go and WHAT to cover. All prose is yours.
> Format: Verdana 10pt, double spacing; margins L=4cm, others 2.54cm; 10,000–15,000 words
> (main text only); Harvard referencing. Six chapters below.

## Chapter 1 — Introduction (10% "Context")
Cover: what IoT is and why it's insecure; the problem (detecting malicious IoT traffic);
why it matters (Mirai-scale botnets). Then your **SMART aims/objectives** and **3 research
questions**. End with a one-paragraph overview of the remaining chapters.
Figures: optional — a simple diagram of the IoT threat / your pipeline.
Citations: Antonakakis et al. (2017) Mirai; an IoT security overview; the IoT-23 dataset.

## Chapter 2 — Literature Review (10%)
Cover: (a) ML for intrusion detection, (b) the explainability gap — most IDS models are
black boxes a SOC can't act on. Build toward YOUR gap: explainable + actionable detection.
End by stating the research questions as the culmination of the review.
Figures/tables: a small comparison table of prior approaches (method, dataset, explainable?).
Citations: ML-IDS survey, SHAP (Lundberg & Lee 2017), prior IoT-23 studies.

## Chapter 3 — New Ideas & Approach (20%)
Cover: your methodology = a data-science workflow (EDA → preprocessing → modelling →
evaluation → explainability → mitigation). Justify **feature selection** (security reasons),
the **encoding/cleaning plan**, **model choice** (LogReg baseline vs RF primary), the
**evaluation strategy** (why AUPRC/recall, not accuracy), and a **PSEL** section
(professional/social/ethical/legal). This is design — describe what you WILL do and why.
Figures: methodology/pipeline diagram; the feature table (keep vs drop, with justification).

## Chapter 4 — Implementation / Investigation (20%)
Cover: what you actually built, notebook by notebook, with a narrative of the process —
including **challenges and how you solved them** (markers reward this honesty):
- EDA loader first sampled only benign files → fixed to sample all 23 captures.
- Output figures folder didn't exist → os.makedirs.
- Realising accuracy was misleading under imbalance → switched metric strategy.
- Repo corruption on OneDrive → moved off OneDrive (process/tooling challenge).
**Verification steps to describe:** label value-counts sanity checks; missing-value audit;
stratified split preserving class balance; fit-transformers-on-train-only to prevent leakage;
notebook re-runs reproducible via random_state.
Figures (place HERE): EDA — class_distribution, attack_type_distribution, protocol,
conn_state, service, numeric_feature_distributions. Plus a before/after preprocessing summary.

## Chapter 5 — Evaluation (part of 20% "Evaluation & Conclusions")
Cover: define the metrics; present results; **then the critical part** — the leakage
investigation. Tell the story: RF won (AUPRC 0.998) → suspicion → grouped split dropped it
to ~0.75 → SHAP showed destination port dominating → conclusion that the random split was
leaky and the model generalises weakly to unseen captures. Then **RQ3**: attack types →
MITRE ATT&CK → mitigations. Discuss limitations honestly.
Figures (place HERE): confusion_matrices; precision_recall_curves; model_comparison table;
rf_grouped_confusion + generalisation_comparison; shap_importance_bar; shap_beeswarm; the
local SHAP explanation; the mitigation mapping table.

## Chapter 6 — Conclusions
Cover: answer each RQ explicitly; revisit aims/objectives; state successes and limitations
(leakage, weak cross-capture generalisation, sampling); future work (group-aware training,
drop leaky features, multiclass, more datasets).

## Abstract (write LAST)
~200–300 words: problem, what you did, key result (incl. the leakage finding), conclusion.
Write it last, once the chapters exist.

---

## Starter references (VERIFY each in Harvard before use)
- **IoT-23 dataset** — Garcia, S., Parmisano, A. & Erquiaga, M.J. (2020) *IoT-23: A labeled
  dataset with malicious and benign IoT network traffic*. Zenodo. DOI 10.5281/zenodo.4743746. ✓verified
- **Mirai** — Antonakakis, M. et al. (2017) *Understanding the Mirai Botnet*. 26th USENIX
  Security Symposium, pp.1093–1110. ✓verified
- **SHAP** — Lundberg, S.M. & Lee, S.-I. (2017) *A Unified Approach to Interpreting Model
  Predictions*. NeurIPS 30. (verify exact pages)
- **Random Forest** — Breiman, L. (2001) *Random Forests*. Machine Learning 45(1), pp.5–32.
- **PR vs ROC under imbalance** — Saito, T. & Rehmsmeier, M. (2015) *The Precision-Recall Plot
  Is More Informative than the ROC Plot When Evaluating Binary Classifiers on Imbalanced
  Datasets*. PLoS ONE 10(3). (justifies AUPRC over accuracy)
- **Zeek/Bro** — Paxson, V. (1999) *Bro: A System for Detecting Network Intruders in
  Real-Time*. Computer Networks 31(23–24).
- **MITRE ATT&CK** — Strom, B.E. et al. (2018) *MITRE ATT&CK: Design and Philosophy*. MITRE.
- **ML methods textbook** — Hastie, Tibshirani & Friedman (2009) *The Elements of Statistical
  Learning*. (for LogReg, RF, RobustScaler concepts)
- Find via Google Scholar: 1–2 recent (2021+) surveys of *machine learning for IoT intrusion
  detection*, and 1–2 papers that used IoT-23, so you can position your work against them.
