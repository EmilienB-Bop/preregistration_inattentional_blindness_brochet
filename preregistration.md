# Preregistration: Benchmarking Dynamic Inattentional Blindness on the Web: Methodological Standardization, Signal Detection Decomposition, and Multiverse Robustness Mapping

## 1. Administrative Information

* **Working Title:** Benchmarking Dynamic Inattentional Blindness on the Web: Methodological Standardization, Signal Detection Decomposition, and Multiverse Robustness Mapping
* **Authors:** Émilien Brochet, Julien Tardieu, Céline Lemercier
* **Affiliation:** Laboratoire CLLE (CNRS, Université de Toulouse Jean Jaurès), France
* **Ethical Approval:** Comité d’Éthique de la Recherche de Toulouse (Avis n° 2026_1242, 18/02/2026)
* **Target Journal Category:** Empirical / Methodological Focus in Experimental Psychology and Cognitive Science (*Behavior Research Methods*, Psychonomic Society / Springer Nature)
* **Public Repository Architecture:** Open Science Framework (OSF) time-stamped project hosting client-side jsPsych scripts, dynamic SVG assets, Firebase Realtime Database schemas, reproducible synthetic datasets, and parameterized Quarto/R pipelines

---

## 2. Theoretical Background & Methodological Rationale

Research using dynamic Multiple Object Tracking (MOT) inattentional blindness (IB) paradigms has historically relied on post-hoc dichotomous probes ("Did you notice anything unusual? YES/NO") without systematically verifying observer criterion shifts or false alarm rates. Furthermore, previous web-based implementations frequently introduced uncalibrated hardware timing artifacts (e.g., frame rate discrepancies between 60 Hz and 120/144 Hz displays), failed to screen mobile/touchscreen devices, and neglected online behavioral interference on primary tracking tasks.

This study implements six critical methodological advancements tailored for standardization in *Behavior Research Methods*:

1. **Signal Detection Theory (SDT) Framework:** Implementing a genuine signal-absent catch baseline (`variant: 'none'`) to decouple true perceptual sensitivity ($d'$) from conservative response bias ($c$).
2. **Multidimensional Factorial Salience:** Systematically manipulating continuous kinematic matching (attentional set) alongside discrete morphological, chromatic, and temporal salience features (shape, color, pulsing size) to test additive versus subadditive capture models.
3. **Implicit Online Behavioral Tracking:** Assessing primary-task tracking accuracy variations between baseline and critical phases to detect attentional capture in observers who deny conscious noticing.
4. **Graded Feature Accessibility & Metacognitive Confidence:** Probing forced-choice feature identification (shape, color, size dynamics) alongside continuous subjective confidence (0–100 sliders) to quantify implicit residual perception and metacognitive dissociation.
5. **Technical Standardization & Client-Side Integrity:** Enforcing client-side hardware refresh rate calibration (sampling 60 frames to verify 60 Hz), animation step recalculation via continuous delta time ($\Delta t$), frame drop logging ($\Delta t > 25\text{ ms}$), physical exclusion of mobile/tablet devices via User-Agent and viewport screening, and real-time logging of window blur and fullscreen exit events.
6. **Data Integrity & Bot Screening:** Embedding a client-side hidden honeypot trap field alongside sub-second submission response time screening ($RT < 1200\text{ ms}$) to identify automated spam submissions before analysis.

---

## 3. Hypotheses

### Hypothesis 1: Kinematic Attentional Set Gating (Speed Congruence)

Explicit detection rates and perceptual sensitivity ($d'$) will be significantly higher when the unexpected stimulus speed matches the attended target speed (Match condition: -200 px/s) compared to when it matches the distractor speed (Mismatch condition: -80 px/s).

### Hypothesis 2: Multidimensional Salience Modulation and Additivity

Physical feature salience will independently modulate explicit detection probability:

* Stimuli deviating from target/distractor baseline features (red color vs. black, triangular shape vs. circle, dynamic 2 Hz pulsing vs. fixed size) will yield higher detection rates than neutral stimuli.
* **Feature Summation:** Combined feature deviations (e.g., color + shape + pulsing) will yield monotonically increasing detection rates compared to single-feature deviations, testing whether salience dimensions operate via additive perceptual channels or saturate subadditively.

### Hypothesis 3: Attentional Set $\times$ Salience Interaction

Attentional set congruence will moderate the impact of physical salience:

* Highly salient compound stimuli (e.g., pulsing red triangle) will partially bypass attentional gating, diminishing the relative advantage of speed congruence.
* Conversely, for low-salience stimuli (black fixed circles), detection will depend almost exclusively on target speed congruence.

### Hypothesis 4: Primary-Task Performance Cost (Implicit Capture)

The presence of the unexpected stimulus will produce a performance cost on the primary counting task (drop in bounce-counting accuracy on Critical Trial 3 relative to pre-critical baseline Trials 1 & 2):

* This cost will be a function of attentional set congruence (larger drop in Match vs. Mismatch).
* This selective cost will remain evident specifically among participants who report not having consciously seen the unexpected stimulus (*non-noticers*), reflecting implicit resource allocation without explicit awareness.

### Hypothesis 5: Conservative Response Bias in Classical IB Probes

Signal detection analysis on the critical trial (comparing unexpected-stimulus-present conditions against the signal-absent `none` catch condition) will reveal a significantly positive response criterion ($c > 0$), confirming that traditional IB reporting exhibits a strong conservative response bias.

### Hypothesis 6: Sub-threshold Feature Extraction & Metacognitive Dissociation

Among self-reported *non-noticers* (observers answering "NON" to the primary detection question):

* Feature forced-choice performance (shape, color, size dynamics) will exceed theoretical chance levels (33.33% for 3-alternative forced choice), corroborating implicit visual extraction without reportable awareness.
* Observers' self-rated confidence for these feature judgments will remain significantly lower than confidence ratings provided by *noticers*, demonstrating an empirical metacognitive dissociation.

### Hypothesis 7: Exposure Duration Invariance (Quantification of Null Evidence)

Controlling for attentional set congruence, raw physical exposure duration (10.25 s for slow unexpected stimulus vs. 4.10 s for fast unexpected stimulus) will exert no systematic independent effect on explicit detection. Evidence for invariance will be confirmed via Bayes Factors in favor of the null hypothesis ($BF_{01} \ge 3.0$) and Two One-Sided Tests (TOST) within predefined equivalence bounds ($\Delta OR \in [0.67, 1.50]$).

---

## 4. Experimental Design

* **Task Paradigm:** Dynamic Multiple Object Tracking (MOT) implemented in jsPsych (v7.x) and HTML5 Canvas ($800 \times 600\text{ px}$, `#525252` background).
* **Primary Task Attentional Set:** 8 black circles (radius 20 px) move continuously within the canvas. Participants are instructed to track and count the wall bounces of the **4 fastest circles (200 px/s)** while ignoring the 4 slow distractors (80 px/s).
* **Kinematic Congruence Factor (`speedcondition`, Between-Subjects, 2 levels):**
* `Match`: Unexpected stimulus speed is -200 px/s (horizontal right-to-left trajectory along the vertical midline, matching attended target speed).
* `Mismatch`: Unexpected stimulus speed is -80 px/s (matching ignored distractor speed).


* **Stimulus Salience & Catch Factor (`variant`, Between-Subjects, 9 levels, uniform random allocation):**
1. `none` (Signal-absent catch trial: no unexpected stimulus appears across Trials 3–5).
2. `circle_black_fixed` (Baseline neutral unexpected stimulus).
3. `circle_black_pulsing` (Temporal dynamic salience: $\pm 10\%$ radius oscillation at 2 Hz).
4. `circle_red_fixed` (Chromatic salience: `#cc0000`).
5. `circle_red_pulsing` (Chromatic + temporal dynamic salience).
6. `triangle_black_fixed` (Morphological salience).
7. `triangle_black_pulsing` (Morphological + temporal dynamic salience).
8. `triangle_red_fixed` (Morphological + chromatic salience).
9. `triangle_red_pulsing` (Compound maximum salience: shape + color + pulsing).


* **Trial Structure:**
* **Screen Calibration & Demographics:** Frame-rate sampling (60 frames), display geometry logging, honeypot validation, and demographic reporting.
* **Practice:** Exactly 2 trials (20 s each, tracking 4 fast circles, immediate percentage feedback, no unexpected stimulus).
* **Pre-critical (Trials 1 & 2):** 2 trials (30 s each, tracking 4 fast circles, target bounce counting only, no unexpected stimulus).
* **Critical (Trial 3):** 1 trial (30 s, unexpected stimulus trajectory begins at $t = 10\text{ s}$ except in `none`). Primary bounce report followed by the comprehensive IB query battery.
* **Divided Attention (Trial 4):** 1 trial (30 s, identical display to Trial 3, dual tracking bounce report and IB query battery).
* **Full Attention (Trial 5):** 1 trial (30 s, tracking instruction discontinued; passive visual observation followed by IB query battery).
* **Debriefing:** Query assessing prior knowledge of selective attention or IB paradigms.



---

## 5. Sampling Plan & Sample Size Justification

* **Target Cell Sample Size:** Exactly 100 valid, fully retained participants per experimental cell across the 18 between-subjects cells (2 Congruence $\times$ 9 Salience variants):

$$N_{\text{analytical}} = 18 \times 100 = 1{,}800\text{ participants}$$

* **Power & Precision Justification:**
* With $N = 100$ per cell, logistic regression models have $> 92\%$ power ($\alpha = .05$, two-tailed) to detect small-to-moderate odds ratio effects ($OR \ge 1.70$) between salience variants and speed congruence levels.
* For the catch-trial condition (`none`, $n = 200$), the false alarm rate ($FA$) is estimated with standard error $SE < 0.025$.
* For Bayesian null assessments ($BF_{01}$ on exposure duration invariance), $N = 900$ per speed condition guarantees sensitivity to detect shifts greater than $d = 0.15$ with $BF_{01} > 10$.


* **Stopping Rule & Attrition Management:** Anticipating a $40\text{--}50\%$ attrition rate due to strict tracking accuracy thresholds, honeypot bot detection, hardware flags, and prior knowledge exclusions, data collection will terminate automatically once the Firebase database logs exactly $N = 3{,}200$ completed sessions.

---

## 6. Variables & Measurements

### 6.1 Dependent Variables (Critical Trial 3)

1. **Explicit Detection (`participant_response_ib`):** Dichotomous response ("OUI" vs. "NON") to *"Avez-vous vu quelque chose d'inhabituel sur cet essai ?"*
2. **Detection Confidence (`confidence_detection`):** Continuous visual slider rating from 0 ("NON, j'ai des doutes...") to 100 ("OUI, je suis sûr·e !").
3. **Feature Discrimination Probes (3-Alternative Forced Choice):**
* Shape (`participant_response_shape`): Circle vs. Triangle vs. "Rien vu".
* Color (`participant_response_color`): Black vs. Red vs. "Rien vu".
* Size Dynamics (`participant_response_size`): Fixed vs. Pulsing vs. "Rien vu".


4. **Feature Confidence Sliders:** Individual continuous ratings (0–100, "Faible certitude" to "Totale certitude") recorded for shape (`confidence_shape`), color (`confidence_color`), and size (`confidence_size`).
5. **Primary-Task Bounce Counting Accuracy (%):**

$$\text{Accuracy}_t = \max\left(0,\, 100 - \frac{\vert{}\text{Reported Count}_t - \text{True Target Bounces}_t\vert{}}{\text{True Target Bounces}_t} \times 100\right)$$

6. **Primary-Task Cost Index:** Mean Pre-critical Accuracy (Trials 1 & 2) minus Critical Trial 3 Accuracy.

---

## 7. Data Exclusion Criteria

Prior to confirmatory analyses, data will be filtered according to the following preregistered criteria:

1. **Primary-Task Non-Compliance:** Participants failing to achieve $\ge 80\%$ mean bounce-counting accuracy on pre-critical trials (Trials 1 & 2) or on Trial 3.
2. **Prior Paradigm Knowledge:** Participants responding "Oui" to having prior knowledge of selective attention or IB paradigms (`participant_prior_knowledge == "Oui"`).
3. **Full-Attention Verification Failure:** Participants in unexpected-stimulus-present conditions who fail to report noticing the stimulus on Trial 5 (full attention). In the catch condition (`none`), participants reporting an unexpected stimulus on Trial 5 are classified as chronic false alarmers and excluded from primary sensitivity comparisons.
4. **Technical Exclusions:** Display refresh rate deviations ($\vert{}\text{measured\_refresh\_rate} - 60\text{ Hz}\vert{} > 4\text{ Hz}$), excessive dropped frames ($> 5\%$ frames exceeding 25 ms inter-frame interval), or logged window `blur` or `fullscreenexit` events during tracking trials.
5. **Bot Flag Exclusions:** Any session triggering the hidden honeypot input field (`user_contact_confirmation`) or exhibiting submission response times below human feasibility ($RT < 1200\text{ ms}$ on demographic inputs; `is_bot_detected == true`).

---

## 8. Confirmatory Statistical Analysis Plan

### 8.1 Confirmatory Model 1: Logistic Regression of Explicit Noticing

A generalized linear model (GLM, binomial family, logit link) will model explicit detection (`detected_raw = 1` vs. `0`) on Critical Trial 3 across all stimulus-present conditions:

$$\text{logit}(P) = \beta_0 + \beta_1 (\text{Congruence}) + \beta_2 (\text{Color}) + \beta_3 (\text{Shape}) + \beta_4 (\text{Dynamics}) + \beta_5 (\text{Congruence} \times \text{Salience})$$

* **Predictor Coding:**
* $\text{Congruence}$: Sum-coded (Match $= +0.5$, Mismatch $= -0.5$).
* $\text{Color}$: Red $= +0.5$, Black $= -0.5$.
* $\text{Shape}$: Triangle $= +0.5$, Circle $= -0.5$.
* $\text{Dynamics}$: Pulsing $= +0.5$, Fixed $= -0.5$.


* **Model Comparison:** Nested model comparisons (Likelihood Ratio Tests and AIC/BIC) will assess whether an additive model of salience features accounts for the data or if significant superadditive/subadditive interaction terms exist.

### 8.2 Confirmatory Model 2: Signal Detection Theory (SDT) & Criterion Analysis

* Using the `none` catch condition, the False Alarm rate ($FA$) will be computed as the proportion of "OUI" responses when no stimulus appeared.
* Hit rates ($H$) will be calculated for each of the 8 stimulus-present variant conditions.
* $d'$ and $c$ will be computed per condition using Hautus (1995) log-linear correction:

$$H_{\text{adj}} = \frac{\text{Hits} + 0.5}{N_{\text{signal}} + 1}, \quad FA_{\text{adj}} = \frac{\text{False Alarms} + 0.5}{N_{\text{catch}} + 1}$$

$$d' = \Phi^{-1}(H_{\text{adj}}) - \Phi^{-1}(FA_{\text{adj}}), \quad c = -0.5 \times \left[\Phi^{-1}(H_{\text{adj}}) + \Phi^{-1}(FA_{\text{adj}})\right]$$

* A one-sample two-tailed $t$-test (and Bayesian equivalent) will test $H_0: c = 0$ against $H_1: c > 0$ across conditions to confirm whether observers operate under a significantly conservative reporting threshold.

### 8.3 Confirmatory Model 3: Implicit Attention Capture (Primary-Task Cost)

A 2 (Phase: Baseline Pre-Critical vs. Critical Trial 3, within-subjects) $\times$ 2 (Congruence: Match vs. Mismatch, between-subjects) mixed-design ANOVA (and linear mixed-effects model) will be performed on bounce-counting accuracy:

* Tested specifically on the subpopulation of self-reported **non-noticers** (participants responding "NON" to the primary probe on Trial 3).
* A significant Phase $\times$ Congruence interaction will confirm implicit perceptual allocation driven by attentional set in the absence of conscious report.

### 8.4 Confirmatory Model 4: Sub-threshold Feature Sensitivity

Among self-reported non-noticers in stimulus-present conditions:

* Proportions of correct identifications for shape, color, and size dynamics will each be evaluated against chance ($1/3 \approx 0.333$) using exact binomial tests.
* Independent-samples Welch $t$-tests and Bayesian Mann-Whitney rank tests will evaluate confidence ratings of non-noticers versus noticers to formally verify the metacognitive dissociation.

### 8.5 Confirmatory Model 5: Bayesian Invariance on Exposure Duration

To test whether exposure duration modulates detection independently of attentional set:

* A Bayesian logistic regression testing the main effect of stimulus speed (80 px/s vs. 200 px/s) while controlling for Congruence.
* Estimation of $BF_{01}$ using default Cauchy priors ($r = \sqrt{2}/2$). Evidence for invariance is defined as $BF_{01} \ge 3.0$ and equivalence testing (TOST) within the bounds $\Delta OR \in [0.67, 1.50]$.

---

## 9. Multiverse Specification Pipeline (320 Analytical Universes)

To evaluate the stability of the congruence effect against researcher degrees of freedom, the primary GLM will be executed across a fully crossed **320-cell multiverse** ($2 \times 8 \times 2 \times 10 = 320\text{ universes}$):

```
                                  MULTIVERSE PIPELINE (320 Universes)
 ┌──────────────────────┐   ┌──────────────────────┐   ┌──────────────────────┐   ┌──────────────────────┐
 │   Prior Knowledge    │   │  Accuracy Threshold  │   │    Full Attention    │   │  Detection Criteria  │
 │      (2 levels)      │   │      (8 levels)      │   │      (2 levels)      │   │     (10 levels)      │
 ├──────────────────────┤   ├──────────────────────┤   ├──────────────────────┤   ├──────────────────────┤
 │ 1. Exclude prior     │   │ 1. No filter         │   │ 1. Exclude deniers   │   │ 1. Just say YES (T3) │
 │ 2. Retain all        │   │ 2. >= 20% accuracy   │   │ 2. Retain all        │   │ 2. Shape correct (T3)│
 │                      │   │ 3. >= 30% accuracy   │   │                      │   │ 3. Color correct (T3)│
 │                      │   │ 4. >= 40% accuracy   │   │                      │   │ 4. Size correct (T3) │
 │                      │   │ 5. >= 50% accuracy   │   │                      │   │ 5. Shape+Color (T3)  │
 │                      │   │ 6. >= 60% accuracy   │   │                      │   │ 6. Shape+Size (T3)   │
 │                      │   │ 7. >= 70% accuracy   │   │                      │   │ 7. Color+Size (T3)   │
 │                      │   │ 8. >= 80% accuracy   │   │                      │   │ 8. All correct (T3)  │
 │                      │   │                      │   │                      │   │ 9. All correct (T4)  │
 │                      │   │                      │   │                      │   │ 10. All correct (T5) │
 └──────────┬───────────┘   └──────────┬───────────┘   └──────────┬───────────┘   └──────────┬───────────┘
            └──────────────────────────┼──────────────────────────┴──────────────────────────┘
                                       ▼
                   Specification Curve & Alluvial Mapping (320 GLMs)

```

### Multiverse Operational Steps:

1. **Model Estimation:** Fit a binomial GLM ($P(\text{Detection}) \sim \text{Congruence}$) across every universe $u \in [1, 320]$.
2. **Specification Curve Display:** Plot all 320 odds ratio point estimates with 95% confidence intervals sorted by effect magnitude, displaying underlying analytical choices along the specification matrix.
3. **Alluvial Decision Flow:** Generate an alluvial flux diagram categorizing paths into significant congruent ($OR > 1, p < .05$, red), non-significant (grey), and the classical preregistered baseline pathway (dark blue).
4. **Bootstrapped Non-Parametric Significance Testing:** Execute a permutation test (5,000 resamples permuting Congruence labels on the raw dataset) to calculate the median odds ratio, proportion of significant universes, and a global multiverse $p$-value.

---

## 10. Open Practices & Reproducibility Declarations

* **Open Materials & Script Availability:** Verbatim jsPsych task scripts, canvas rendering modules, calibration code, and mock R analysis pipelines will be released under an open MIT License on GitHub and archived on Zenodo.
* **Raw Data Repository:** Fully de-identified trial-by-trial CSV logs, frame timing durations, slider values, and response counts will be uploaded to an anonymized OSF repository for double-blind peer review.
* **Pre-registration Integrity:** Any post-hoc exploratory derivations or analytical pipeline adjustments arising during peer review will be explicitly logged in an online OSF amendment tracking matrix, preserving strict demarcation between confirmatory hypotheses and exploratory insights.
