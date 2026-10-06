# Preregistration: Disentangling Attentional Set, Multidimensional Stimulus Salience, and Response Bias in Dynamic Inattentional Blindness: A Signal Detection Approach

## 1. Administrative Information

* **Working Title:** Disentangling Attentional Set, Multidimensional Stimulus Salience, and Response Bias in Dynamic Inattentional Blindness: A Signal Detection Approach
* **Authors:** Émilien Brochet, Julien Tardieu, Céline Lemercier
* **Affiliation:** Laboratoire CLLE (CNRS, Université de Toulouse Jean Jaurès), France
* **Ethical Approval:** Comité d’Éthique de la Recherche de Toulouse (Avis n° 2026_1242, 18/02/2026)
* **Target Journal Category:** Empirical / Methodological Focus in Experimental Psychology and Cognitive Science (e.g., *Behavior Research Methods*, *Consciousness and Cognition*, *Attention, Perception, & Psychophysics*)

---

## 2. Theoretical Background & Methodological Rationale

Research using the dynamic Multiple Object Tracking (MOT) inattentional blindness (IB) paradigm has historically relied on post-hoc dichotomous probes ("Did you notice anything unusual? YES/NO") without systematically verifying observer criterion shifts or false alarm rates. Furthermore, previous studies often conflated bottom-up physical salience with top-down attentional control settings, or varied only single feature dimensions (e.g., luminance or isolated speed differences) without evaluating feature summation, interactive gating, or online implicit interference.

This study implements five critical methodological advancements in sustained IB research:

1. **Signal Detection Theory (SDT) Framework:** Implementing a genuine catch-trial baseline (`variant: 'none'`) to decouple true perceptual sensitivity ($d'$) from conservative response bias ($c$).
2. **Multidimensional Factorial Salience:** Systematically manipulating continuous kinematic matching (attentional set) alongside discrete morphological, chromatic, and temporal salience features (shape, color, pulsing size) to test additive vs. subadditive capture models.
3. **Implicit Online Behavioral Tracking:** Assessing primary-task tracking accuracy variations to detect attention capture in observers who deny conscious noticing.
4. **Graded Feature Accessibility & Metacognitive Confidence:** Probing forced-choice feature identification (shape, color, size dynamics) alongside continuous subjective confidence to quantify implicit residual perception.
5. **Technical Standardization:** Enforcing client-side hardware refresh rate calibration (60 Hz verification), screen geometry logging, and strict exclusion of mobile/tablet devices.

---

## 3. Hypotheses

### Hypothesis 1: Attentional Set Gating (Kinematic Congruence)

Explicit detection rates and perceptual sensitivity ($d'$) will be significantly higher when the unexpected stimulus (US) speed matches the attended target speed (Match condition: fast-fast or slow-slow) compared to when it matches the distractor speed (Mismatch condition).

### Hypothesis 2: Multidimensional Salience Modulation and Additivity

Physical feature salience will independently modulate explicit detection probability:

* Stimuli deviating from target/distractor baseline features (red color vs. black, triangular shape vs. circle, dynamic 2 Hz pulsing vs. fixed size) will yield higher detection rates than neutral stimuli.
* **Feature Summation:** Combined feature deviations (e.g., color + shape + pulsing) will yield monotonically increasing detection rates compared to single-feature deviations, testing whether salience dimensions operate via additive perceptual channels or saturate subadditively.

### Hypothesis 3: Attentional Set $\times$ Salience Interaction

Attentional set congruence will moderate the impact of physical salience:

* Highly salient features (e.g., pulsing red triangle) will partially bypass attentional gating, diminishing the relative advantage of speed congruence.
* Conversely, for low-salience stimuli (black fixed circles), detection will depend almost exclusively on target speed congruence.

### Hypothesis 4: Primary-Task Performance Cost (Implicit Capture)

The presence of the US will produce a performance cost on the primary counting task (drop in bounce-counting accuracy on Critical Trial 3 relative to pre-critical trials):

* This cost will be function of both attentional set congruence (larger drop in Match vs. Mismatch) and stimulus salience (monotonically greater impairment as salience features summate).
* This selective cost will remain evident even among participants who report not having consciously seen the US (*non-noticers*), reflecting implicit resource allocation without explicit awareness.

### Hypothesis 5: Conservative Response Bias in Classical IB Probes

Signal detection analysis on the critical trial (comparing US-present conditions against the US-absent `none` catch condition) will reveal a significantly positive response criterion ($c > 0$), confirming that traditional IB reporting exhibits a strong conservative response bias (participants are fundamentally biased toward responding "NO" unless confidence is high).

### Hypothesis 6: Subliminal Feature Extraction & Metacognitive Dissociation

Among self-reported *non-noticers* (observers answering "NO" to the primary detection question):

* Feature forced-choice performance (shape, color, size dynamics) will exceed theoretical chance levels (33.3% for 3-alternative forced choice), corroborating implicit visual extraction without reportable awareness.
* Observers' self-rated confidence for these feature judgments will remain significantly lower than confidence ratings provided by *noticers*, demonstrating a true metacognitive dissociation.

---

## 4. Experimental Design

* **Task Paradigm:** Dynamic Multiple Object Tracking (MOT) in jsPsych, rendered on a canvas element ($800 \times 600\text{ px}$, `#525252` background).
* **Attentional Set Factor (Between-Subjects, 2 levels):**
* `speedcondition = 'slow'`: 4 targets move at 80 px/s; 4 distractors move at 200 px/s.
* `speedcondition = 'fast'`: 4 targets move at 200 px/s; 4 distractors move at 80 px/s.


* **Stimulus Salience & Catch Factor (`variant`, Between-Subjects, 9 levels):**
1. `none` (Catch trial: no US appears across Trials 3–5).
2. `circle_black_fixed` (Baseline neutral US).
3. `circle_black_pulsing` (Temporal dynamic salience: $\pm 10\%$ radius oscillation at 2 Hz).
4. `circle_red_fixed` (Chromatic salience).
5. `circle_red_pulsing` (Chromatic + temporal dynamic salience).
6. `triangle_black_fixed` (Morphological salience).
7. `triangle_black_pulsing` (Morphological + temporal dynamic salience).
8. `triangle_red_fixed` (Morphological + chromatic salience).
9. `triangle_red_pulsing` (Compound maximum salience: shape + color + pulsing).



For all US-present conditions, US velocity is randomly set to slow (-80 px/s) or fast (-200 px/s), crossing horizontally from right to left starting at $t = 10\text{ s}$ into the 30-second trial.

* **Trial Structure:**
* **Practice:** 2 trials (20 s, 80% accuracy threshold required, immediate precision feedback).
* **Pre-critical (Trials 1 & 2):** 2 trials (30 s, target bounce counting only).
* **Critical (Trial 3):** 1 trial (30 s, US trajectory active except in `none`). Primary bounce count report, followed by the comprehensive IB query battery.
* **Divided Attention (Trial 4):** 1 trial (identical display to Trial 3, primary count + probe).
* **Full Attention (Trial 5):** 1 trial (passive monitoring, counting discontinued, identical visual display).



---

## 5. Sampling Plan & Sample Size Justification

* **Cell Size:** 100 valid, fully retained participants per condition across the 9 variant groups (stratified across target tracking speeds):

$$N_{\text{analytical}} = 9 \times 100 = 900\text{ participants}$$


* **Power Justification:** With $N = 100$ per cell, logistic regression models have $> 90\%$ power ($\alpha = .05$) to detect small-to-moderate odds ratio effects ($OR \ge 1.65$) between salience variants and speed congruence levels, as well as adequate precision to estimate false alarm rates ($FA$) in the catch condition with standard errors $< 0.03$.
* **Attrition Management:** Anticipating a $\sim 40\text{--}50\%$ attrition rate due to strict accuracy thresholds, prior knowledge exclusions, and online dropouts, data collection will run until approximately 1,600 to 1,800 total sessions have been initialized on Firebase Realtime Database.

---

## 6. Variables & Measurements

### 6.1 Dependent Variables (Critical Trial 3)

1. **Explicit Detection (`participant_response_ib`):** Dichotomous response ("OUI" vs. "NON").
2. **Detection Confidence (`confidence_detection`):** Continuous visual slider rating from 0 ("NON, j'ai des doutes...") to 100 ("OUI, je suis sûr.e !").
3. **Feature Probes (3-Alternative Forced Choice):**
* Shape: Circle vs. Triangle vs. "Rien vu".
* Color: Black vs. Red vs. "Rien vu".
* Size: Fixed vs. Pulsing vs. "Rien vu".


4. **Feature Confidence Sliders:** Individual continuous ratings (0–100) for shape, color, and size judgments.
5. **Primary-Task Accuracy (%):**

$$\text{Accuracy} = \max\left(0,\, 100 - \frac{\vert{}\text{Reported Count} - \text{True Target Bounces}\vert{}}{\text{True Target Bounces}} \times 100\right)$$


6. **Task Cost Index:** Mean Pre-critical Accuracy (Trials 1 & 2) minus Critical Trial 3 Accuracy.

---

## 7. Data Exclusion Criteria

Prior to confirmatory analyses, data will be filtered according to the following preregistered criteria:

1. **Primary-Task Non-Compliance:** Participants failing to achieve $\ge 80\%$ mean bounce-counting accuracy on pre-critical trials (Trials 1 & 2) or on Trial 3.
2. **Prior Paradigm Knowledge:** Participants responding "Oui" to having prior knowledge of selective attention or IB paradigms (`participant_prior_knowledge == "Oui"`).
3. **Full-Attention Verification Failure:** Participants in US-present conditions who fail to detect the US on Trial 5 (full attention). In the catch condition (`none`), participants reporting an unexpected stimulus on Trial 5 are classified as high-rate false alarmers and excluded from primary sensitivity comparisons.
4. **Technical Exclusions:** Display refresh rate deviations ($\vert{}\text{measured\_refresh\_rate} - 60\vert{} > 4\text{ Hz}$), excessive dropped frames ($> 5\%$ frames exceeding 25 ms inter-frame interval), or logged window blur / fullscreen exit events during tracking trials.

---

## 8. Confirmatory Statistical Analysis Plan

### 8.1 Confirmatory Model 1: Logistic Regression of Explicit Noticing

A generalized linear model (GLM, binomial family, logit link) will model explicit detection (`detection_ib = 1` vs. `0`) on Critical Trial 3 across all US-present conditions:


$$\text{logit}(P) = \beta_0 + \beta_1 (\text{Congruence}) + \sum_{k=1}^3 \beta_{2k} (\text{Salience}_k) + \beta_3 (\text{Congruence} \times \text{Salience})$$

* **Congruence:** Coded as Match (+0.5) vs. Mismatch (-0.5).
* **Salience Contraste Orthogonaux:**
* Contrast 1 (Color): Red (+0.5) vs. Black (-0.5).
* Contrast 2 (Shape): Triangle (+0.5) vs. Circle (-0.5).
* Contrast 3 (Dynamics): Pulsing (+0.5) vs. Fixed (-0.5).


* **Model Comparison:** Nested model comparisons (Likelihood Ratio Tests and AIC/BIC) will assess whether an additive model of salience features accounts for the data or if significant superadditive/subadditive interaction terms exist.

### 8.2 Confirmatory Model 2: Signal Detection Theory (SDT) & Criterion Analysis

* Using the `none` catch condition, the False Alarm rate ($FA$) will be computed as the proportion of "OUI" responses when no US appeared.
* Hit rates ($H$) will be calculated for each of the 8 US-present variant conditions.
* $d'$ and $c$ will be computed per condition using the standard normal quantile function:

$$d' = \Phi^{-1}(H) - \Phi^{-1}(FA), \quad c = -0.5 \times \left[\Phi^{-1}(H) + \Phi^{-1}(FA)\right]$$



*(Log-linear correction applied for extreme proportions).*
* A one-sample two-tailed $t$-test (and Bayesian equivalent) will test $H_0: c = 0$ across conditions to confirm whether observers operate under a significantly conservative reporting threshold ($c > 0$).

### 8.3 Confirmatory Model 3: Implicit Attention Capture (Primary-Task Cost)

A 2 (Phase: Baseline Pre-Critical vs. Critical Trial 3, within-subjects) $\times$ 2 (Congruence: Match vs. Mismatch, between-subjects) $\times$ Salience Level mixed-design ANOVA will be performed on bounce-counting accuracy:

* Tested specifically on the subpopulation of self-reported **non-noticers**.
* A significant Phase $\times$ Congruence interaction will confirm implicit perceptual allocation driven by attentional set in the absence of conscious report.

### 8.4 Confirmatory Model 4: Sub-threshold Feature Sensitivity

Among self-reported non-noticers:

* Proportions of correct identifications for shape, color, and size dynamics will each be evaluated against chance (0.33) using binomial tests.
* A paired $t$-test will evaluate confidence ratings of non-noticers versus noticers to formally verify the metacognitive dissociation.

---

## 9. Exploratory Analyses & Multiverse Pipeline

1. **Multiverse Specification Analysis:** Constructing a 320-pathway specification curve varying counting accuracy cutoffs ($60\%\text{--}90\%$), retention vs. exclusion of full-attention non-noticers, and strict vs. lenient detection definitions.
2. **Bayesian Null Quantifications:** Computing Bayes Factors ($BF_{01}$, default Cauchy prior $r = 0.707$) on non-significant effects (notably physical exposure time differences between 80 px/s and 200 px/s conditions) to distinguish between data insensitivity and true invariance.
3. **Recovery Trajectories:** Tracking detection escalation from Trial 3 (Critical) to Trial 4 (Divided) and Trial 5 (Full) as a function of salience combination.
