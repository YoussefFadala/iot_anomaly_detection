# Project Framing — BRAINSTORMING SCAFFOLD (rewrite in your own words)

> ⚠️ This is idea-generation only (NTU "Green" use of AI). Do NOT paste any of this
> into your report. Use it to understand the shape, then write every line yourself.
> Being able to say these out loud in your own words = marks in the viva/demo.

---

## 1. Problem domain (the "why this matters")
IoT devices are deployed everywhere and are often poorly secured, making them both
frequent targets and launch-points for attacks (e.g. the Mirai botnet). Detecting
malicious traffic on IoT networks is therefore an important security problem.
Supervised machine learning can learn to separate benign from malicious network
flows from labelled data such as IoT-23.

## 2. The gap / novelty (what makes this more than "yet another classifier")
Most ML-based intrusion detection research optimises for accuracy but produces
"black-box" models: a SOC (Security Operations Centre) analyst gets an alert but no
reason for it and no guidance on what to do. The gap this project targets:
**detection that is also explainable and actionable** — it tells the analyst *why*
a flow was flagged (via SHAP) and *what to do* about each attack type (mitigation).

This is your Distinction-shaped angle. The classifier is the vehicle; explainability
+ actionability is the contribution.

## 3. Aim (one sentence — rewrite it)
*Draft:* To design and evaluate an explainable supervised machine-learning approach
for detecting malicious network traffic in IoT environments, that provides security
analysts with interpretable reasons for each detection and practical mitigation
guidance per attack type.

## 4. Objectives (the concrete steps — rewrite each)
1. Review literature on IoT intrusion detection and ML explainability to identify a
   clear research gap and define the research questions.
2. Prepare and analyse the IoT-23 dataset: exploratory analysis, security-justified
   feature selection, and preprocessing.  *(largely done)*
3. Implement two supervised models — Logistic Regression (baseline) and Random
   Forest (primary) — for binary benign/malicious classification.
4. Evaluate the models using imbalance-aware metrics (PR-AUC, F1, confusion matrix)
   and test how well they generalise across different capture files.
5. Apply SHAP to the primary model to explain its decisions in terms a SOC analyst
   can act on.
6. Derive a mitigation recommendation for each attack type present in the dataset.

## 5. Research questions (what the evaluation answers — rewrite each)
- **RQ1.** How effectively can supervised ML (Logistic Regression vs Random Forest)
  distinguish malicious from benign IoT network flows on IoT-23 under class imbalance?
- **RQ2.** Which network-flow features most influence the detection decisions, and can
  SHAP present these in a way that is interpretable and useful to a SOC analyst?
- **RQ3.** Can the attack types detected be mapped to specific, actionable mitigation
  recommendations?

## 6. PSEL — issues to discuss in Chapter 3 (Professional, Social, Ethical, Legal)
You will need a paragraph on each. Starting points (expand in your own words):
- **Professional:** false positives waste analyst time; false negatives miss attacks —
  the cost trade-off and how an explainable model helps triage.
- **Social:** insecure IoT affects ordinary people (home cameras, etc.); better
  detection has societal benefit.
- **Ethical:** network traffic can contain personal data; using a public, de-identified
  research dataset (IoT-23) mitigates this — discuss responsible use and bias.
- **Legal:** monitoring network traffic engages data-protection law (e.g. UK GDPR);
  detectors must be deployed lawfully and proportionately.

---

## Your turn (ownership tasks)
1. Rewrite the Aim in one sentence, your words.
2. Rewrite the 6 objectives so they sound like you and feel achievable by 28 Aug.
3. Keep, cut, or change RQ1–RQ3 — do all three feel answerable with what we're building?
4. Tell me anything here you could NOT yet explain to your supervisor — that's what we cover next.
