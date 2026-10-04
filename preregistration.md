# Preregistration: Salience Dimensions, Attentional Sets, and Signal Detection in Sustained Inattentional Blindness

## 1. Study Information

* **Title:** Testing Feature Salience and Signal Detection in Inattentional Blindness: A Factorial Exploration of Motion, Color, Shape, and Dynamic Pulsing
* **Authors:** Émilien Brochet, Julien Tardieu, Céline Lemercier
* **Date of Preregistration:** October 2026
* **Status:** Prior to data collection

---

## 2. Experimental Design

### 2.1 Overview & Factors

The study employs a dynamic Multiple Object Tracking (MOT) paradigm with a between-subjects factorial design. Observers track and count wall-bounces of four target circles among four distractor circles.

The experimental design manipulates:

1. **Target Tracking Speed (Attentional Set Baseline):**
* Between-subjects factor: `speedcondition` $\in$ {`slow` (80 px/s), `fast` (200 px/s)}. Distractors move at the alternative speed (200 px/s and 80 px/s, respectively).


2. **Unexpected Stimulus (US) Variant & Salience:**
* Randomly assigned between-subjects factor (`variant`, 9 levels):
* **Condition 0 (Catch / Baseline - No US):** `none` (No unexpected stimulus presented on Trials 3 to 5).
* **Condition 1 (Baseline Circle - Fixed):** `circle_black_fixed` (Speed-matched or speed-mismatched).
* **Condition 2 (Dynamic Salience - Pulsing):** `circle_black_pulsing` (Sinusoidal radius oscillation: $\pm 10\%$, 2 Hz).
* **Condition 3 (Static Color Salience - Fixed):** `circle_red_fixed`.
* **Condition 4 (Dynamic Color Salience - Pulsing):** `circle_red_pulsing`.
* **Condition 5 (Shape Salience - Fixed):** `triangle_black_fixed`.
* **Condition 6 (Shape + Dynamic Salience - Pulsing):** `triangle_black_pulsing`.
* **Condition 7 (Shape + Color Salience - Fixed):** `triangle_red_fixed`.
* **Condition 8 (Compound Salience - Pulsing):** `triangle_red_pulsing`.





On trials where a US is present, its velocity is also assigned randomly to either slow (-80 px/s) or fast (-200 px/s), crossing from right to left.

### 2.2 Trial Sequence

* **Practice Phase:** 2 trials (20 s each, 80% accuracy threshold required, immediate performance feedback).
* **Pre-critical Phase (Trials 1 & 2):** 2 trials (30 s each, primary bounce-counting task only, no US).
* **Critical Phase (Trial 3):** 1 trial (30 s, US appears at $t = 10\text{ s}$ except in the `none` condition). Followed by the bounce report, the IB detection battery, and confidence ratings.
* **Divided-Attention Phase (Trial 4):** 1 trial (identical display to Trial 3, primary task + probe).
* **Full-Attention Phase (Trial 5):** 1 trial (passive viewing without bounce counting).

---

## 3. Sampling Plan & Power Analysis

### 3.1 Target Sample Size

* **Target Analytical Sample:** 100 valid participants per condition. Across the 9 variant groups (with balanced tracking speeds), the final retained sample target is:

$$N_{\text{analytic}} = 9 \times 100 = 900\text{ participants}$$


* **Attrition Adjustment:** Based on empirical attrition rates in dynamic online IB experiments (exclusion due to primary-task counting inaccuracy $<80\%$, prior paradigm knowledge, and technical drops), an attrition buffer of $\sim 40\text{--}50\%$ is accounted for. Data collection will stop once the server records approximately **1,500 to 1,800 initiated sessions** or when cell quotas reach 100 valid participants each.

### 3.2 Participant Recruitment & Testing Environment

* Sessions are collected online using automated single-use links.
* **Device Enforcement:** Mobile devices and tablets are programmatically filtered out (`isComputer()` check). Participants must complete the experiment on a desktop/laptop with physical display, keyboard, and mouse.
* Display refresh rates are empirically measured at session start across 60 frames via `requestAnimationFrame` and logged (`measured_refresh_rate`). Screen dimensions and pixel ratios are recorded.

---

## 4. Measured Variables & Indices

### 4.1 Primary Dependent Variables (Critical Trial 3)

* **Explicit Detection Response (`detection_ib`):** Binary report ("YES" vs. "NO") to whether anything unusual was observed.
* **Detection Confidence (`confidence_detection`):** Continuous visual slider rating (0 = "Very doubtful", 100 = "Totally certain").
* **Feature Identification (Forced-Choice Probes):**
* **Shape:** Circle vs. Triangle vs. "Nothing seen" (SVG visual probe).
* **Color:** Black vs. Red vs. "Nothing seen".
* **Size Dynamics:** Fixed vs. Pulsing vs. "Nothing seen".


* **Feature Confidence Ratings:** Continuous sliders (0--100) for Shape, Color, and Size judgments.
* **Strict Noticer Classification:** A participant is classified as a *Strict Noticer* if and only if:
1. They respond "YES" to the initial detection query;
2. They correctly identify the US shape, color, and size dynamics.



### 4.2 Signal Detection Theory (SDT) Metrics

Using the catch trial condition (`variant == 'none'`):

* **Hit Rate ($H$):** Proportion of "YES" responses when the US was present.
* **False Alarm Rate ($FA$):** Proportion of "YES" responses in the `none` condition.
* **Sensitivity Index ($d'$):**

$$d' = \Phi^{-1}(H) - \Phi^{-1}(FA)$$



*(with log-linear corrections applied in cases of extreme proportions, Hautus, 1995).*
* **Response Criterion ($c$):**

$$c = -0.5 \times [\Phi^{-1}(H) + \Phi^{-1}(FA)]$$



### 4.3 Behavioral & Secondary Metrics

* **Primary-Task Accuracy:**

$$\text{Accuracy} = \max\left(0,\, 100 - \frac{\vert{}\text{Reported Count} - \text{True Bounces}\vert{}}{\text{True Bounces}} \times 100\right)$$


* **Primary-Task Implicit Cost:** Difference in accuracy between pre-critical baseline (mean of Trials 1 and 2) and Critical Trial 3.

---

## 5. Exclusion Criteria (Pre-Specified Pipeline)

Participants will be excluded from the confirmatory sample if they meet any of the following criteria:

1. **Primary-Task Inaccuracy:** Mean counting accuracy $< 80\%$ on pre-critical trials (Trials 1 and 2) or $< 80\%$ on Critical Trial 3.
2. **Prior Paradigm Knowledge:** Reporting prior familiarity with inattentional blindness or selective attention tasks (e.g., the invisible gorilla study) on the final debriefing question (`prior_knowledge == "Oui"`).
3. **Full-Attention Failure:** Failure to report the US on Trial 5 (full-attention trial) for conditions where the US is present.
4. **Technical Anomalies:** Excessive frame drops ($> 5\%$ of animation frames exceeding 25 ms inter-frame delta) or exiting fullscreen/losing window focus during tracking trials.

---

## 6. Confirmatory Analysis Plan

### 6.1 Explicit Detection Models

* **Model 1 (Generalized Linear Model - Binomial Family):**
A logistic regression model will predict binary detection (`detection_ib`) on Critical Trial 3 across US-present variants:

$$\text{logit}(P(\text{Detection})) = \beta_0 + \beta_1 (\text{Speed Congruence}) + \beta_2 (\text{Salience Feature}) + \beta_3 (\text{Speed Congruence} \times \text{Salience Feature})$$


* `Speed Congruence` is coded as a factor: Match (Target Speed = US Speed) vs. Mismatch (Target Speed $\neq$ US Speed).
* `Salience Feature` is entered as orthogonal planned contrasts:
* Contrast 1: Dynamic modulation (`pulsing` vs. `fixed`).
* Contrast 2: Chromatic contrast (`red` vs. `black`).
* Contrast 3: Morphological difference (`triangle` vs. `circle`).




* **Model 2 (Signal Detection Comparison):**
Independent $d'$ and $c$ values will be estimated across salience conditions relative to the baseline `none` group. Differences in perceptual sensitivity ($d'$) versus shifts in response criterion ($c$) will be tested using Welch $t$-tests and bootstrapped 95% confidence intervals.

### 6.2 Implicit Processing (Task Cost Analysis)

* Mixed-design ANOVA on Primary-Task Accuracy:
* Within-subjects factor: `Phase` (Pre-critical Baseline vs. Critical Trial 3).
* Between-subjects factor: `Condition` (US-Absent Baseline, Match US, Mismatch US).
* **Planned Comparison:** Focused testing of the interaction contrast assessing whether the drop in tracking accuracy during Trial 3 is selectively amplified in the Match condition among self-reported *non-noticers*.



### 6.3 Bayesian Verification for Null Effects

* In order to avoid conflating "absence of evidence" with "evidence of absence", Bayesian contingency tables and Bayesian regression models (using default Cauchy priors, $r = 0.707$) will be computed for all non-significant main effects (particularly exposure duration and non-matching salience dimensions). $BF_{01} > 3$ will be interpreted as substantial evidence favoring the null hypothesis.

---

## 7. Exploratory Analyses

1. **Multiverse Pipeline Analysis:** Robustness across 320 analytical specifications varying primary-task accuracy thresholds ($60\%\text{--}90\%$), inclusion/exclusion of full-attention deniers, and strict vs. lenient detection criteria.
2. **Feature-Reporting Asymmetries:** Hierarchy of conscious reportability (proportions and confidence distributions) comparing motion, color, shape, and pulsation among partial noticers.
3. **Repeated Exposure Dynamics:** Trajectory of detection recovery across Trial 3, Divided Attention (Trial 4), and Full Attention (Trial 5).
