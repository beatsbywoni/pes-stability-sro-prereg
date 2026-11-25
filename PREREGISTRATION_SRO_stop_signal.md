# Preregistration: Replication of the stop-signal results on post-error slowing in an independent sample with a longer retest interval

Version 1.0, written 2026-11-25 (KST), before any response-time-based quantity of the replication data set was computed.

## 1. Purpose

The main study (a reanalysis of Hedge et al., 2018, exploratory) reported, for the stop-signal task: (a) event-matched post-error slowing (PES; go RT after a failed stop minus after a successful stop) was consistent within a session but its correlation between sessions fell short of what the split-half coefficients allowed (ρ = .69 [.48, .95] over three weeks); (b) go trials after failed stops were not slower than after successful stops, also relative to a local baseline; (c) failed stops occurred during fast stretches of responding; (d) post-signal slowing (after a successful stop minus after a correct go trial) was robust and remained relative to a local baseline; (e) the local-baseline version of event-matched PES had split-half coefficients near zero. This registration tests these results in an independent sample, with another population (online adults), another version of the task, and a longer retest interval, using analyses fixed in advance. It also tests the surprise (orienting) account of post-signal slowing against the goal-priority account with a within-person manipulation of stop-signal probability (Bissett & Logan, 2011).

## 2. Data

- Self-Regulation Ontology retest data (Eisenberg et al., 2019; Enkavi et al., 2019), public at https://github.com/IanEisenberg/Self_Regulation_Ontology, folder `Data/` (commit 4e6e837fb5aaca87ed5914fd9be251156f43eec9): `Complete_02-16-2019/Individual_Measures/stop_signal.csv.gz` (time 1) and `Retest_02-16-2019/Individual_Measures/stop_signal.csv.gz` (time 2).
- Participants: workers present in both files (n = 150 known; Enkavi et al. report a mean retest interval of 111 days, range 60 to 228).
- Task (as coded in the files): rows with `exp_stage == "test"`; 600 trials per session in two runs of 300 (`trial_num` restarts at 0), one run with stop signals on 40% of trials (`condition == "high"`) and one with 20% (`condition == "low"`), run order counterbalanced across participants; stop-signal delay adjusted by a staircase restarting at 250 ms in each run; two response keys (`possible_responses`), `key_press == -1` for no response, `rt == -1` for no response, RT in ms.

**What is known about these data before analysis.** The column structure; the numbers of participants, sessions, runs, and trials; the proportions of stop trials per condition; the run order counts; the range of the stop-signal delay; and, per participant and session, the numbers of failed stops (median about 89) and of errors in other SRO tasks. No RT-based quantity (means, PES, slowing, reliability, or correlations) has been computed from these data by the author. The SRO data files contain post-error-slowing variables for other tasks but none for the stop-signal task; the author has not inspected their values. Enkavi et al. (2019) reported test–retest reliability for SRO stop-signal variables such as SSRT, but not for any post-error or post-signal score. All results of the main study (Hedge data) are known.

## 3. Coding of trials

- Session s ∈ {1, 2}; run = the condition block (`high` or `low`), identified by the restart of `trial_num`.
- Stop trial: `SS_trial_type == "stop"`; failed stop: stop trial with `key_press != -1`; successful stop: stop trial with `key_press == -1`.
- Go trial: `SS_trial_type == "go"`; correct go trial: `key_press == correct_response`; go error: response with the wrong key; go omission: `key_press == -1`.
- Valid RT: 150 to 3,000 ms (as in the main study). A scored trial is a correct go trial with valid RT in the same run as the preceding trial.

## 4. Participants

All participants with test-stage data in both sessions. A participant enters the analysis of a score with at least 10 post-event trials in each session and at least 2 post-event and 2 control trials in each half of the odd/even split of each session (the block-split rule of the main study is not used because the task has two runs that differ in stop-signal probability). Sensitivity analysis: participants who, in both sessions, respond on 25% to 75% of stop trials, omit at most 10% of go trials, and have a mean signal-respond RT below their mean correct go RT (after Verbruggen et al., 2019).

## 5. Scores (per participant and session, pooled over the two runs unless stated)

1. **Event-matched PES (primary):** mean RT of scored go trials after a failed stop minus after a successful stop.
2. **Local-baseline event-matched PES:** for stop trials n whose trials n − 4, n − 1, and n + 1 are correct go trials with valid RT in the same run, RT(n + 1) − RT(n − 4); mean after failed stops minus mean after successful stops; windows that share a trial with an earlier retained window are dropped (failed and successful together). Also RT(n + 1) − RT(n − 1) and the pre-event differences RT(n − 1) and RT(n − 4) (failed minus successful).
3. **Post-signal slowing:** mean RT of scored go trials after a successful stop minus after a correct go trial; and its local-baseline version (windows as in 2, after successful stops versus after correct go trials, non-overlap within each set).
4. **Conventional PES (for continuity, confounded with the signal):** mean RT of scored go trials after any error (failed stop, go error, or go omission) minus after a correct go trial.
5. **Benchmarks:** mean correct go RT; probability of responding on stop trials; SSRT (integration method, go omissions assigned the participant's slowest go RT, pooled over runs).
6. **Post-signal slowing by run:** score 3 computed separately in the high (40%) and low (20%) runs.

## 6. Coefficients

As in the main study (code `stability.py` functions): in each session, 1,000 stratified random splits of post-event and control trials into halves of equal size, each half scored from its own trials; *rel* = mean Spearman–Brown coefficient; *r*~12~ between full scores; ρ = *r*~12~/√(*rel*~1~*rel*~2~); 2,000 bootstrap resamples of participants (seed 20261201) with the split means recomputed in each resample; undefined resamples counted; paired differences on the same resamples. Means per session with 95% percentile bootstrap intervals. Secondary estimator for ρ of score 1: the precision-weighted bivariate measurement-error model of the main study (maximum likelihood, 2,000 participant resamples).

## 7. Hypotheses and decision rules

- **H1 (stability shortfall):** ρ of event-matched PES < 1. Supported if the upper limit of its 95% interval is below 1 (with no more than 5% undefined resamples); not supported otherwise. The point estimate is reported regardless and compared with the main study (.69).
- **H2 (no error-specific slowing in stop-signal):** the local-baseline event-matched PES lies within ±15 ms (smallest effect of interest: about one third of the post-signal slowing in the main study) in each session. Supported if the 90% interval lies within (−15, 15) ms in both sessions; contradicted if the 95% interval excludes 0 with a positive mean in either session; otherwise inconclusive.
- **H3 (post-signal slowing):** raw and local-baseline post-signal slowing > 0. Supported if the lower limits of the 95% intervals exceed 0 in both sessions.
- **H4 (failed stops occur during fast stretches):** RT(n − 1) before failed stops is faster than before successful stops. Supported if the upper limit of the 95% interval is below 0 in both sessions.
- **H5 (local-baseline score not consistent within a session):** the split-half coefficient of local-baseline event-matched PES is lower than that of raw event-matched PES (computed in the same participants). Supported if the paired difference (local minus raw) has an upper 95% limit below 0 in both sessions.
- **H6 (surprise versus goal priority):** raw post-signal slowing (score 3, first definition) differs between the high (40%) and low (20%) runs. The surprise account predicts more slowing in the low run; the goal-priority account (Bissett & Logan, 2011) predicts more slowing in the high run. The paired difference (high minus low) with its 95% interval is reported per session; a positive interval excluding 0 in both sessions favors goal priority, a negative one favors surprise, otherwise inconclusive.

## 8. Further analyses (reported, not tested)

ρ of conventional PES, post-signal slowing, mean correct go RT, probability of responding, and SSRT; local-baseline post-signal slowing by run; paired differences of ρ (event-matched PES minus each); RT at positions −4 to +3 around failed and successful stops; mean change between sessions; the sensitivity sample (Section 4); the precision-weighted ρ.

## 9. Reporting

All tests in Section 7 are reported, whatever their outcome, in the article that reports the main study, labeled as confirmatory, together with deviations from this registration. Code: `code/sro_replication.py` and the functions it uses (`code/`; deposited with this registration; tested only on synthetic data with the structure of the files, all RTs replaced by random draws, before registration).
