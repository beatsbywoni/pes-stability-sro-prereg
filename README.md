# Preregistration: post-error slowing in the stop-signal task, Self-Regulation Ontology retest data

This record fixes, before analysis, the hypotheses, scores, samples, decision rules, and code of a replication of the stop-signal results of a reanalysis of Hedge et al. (2018) on the within-session consistency and between-session stability of post-error slowing.

- `PREREGISTRATION_SRO_stop_signal.md`: the registration (hypotheses H1 to H6 and decision rules).
- `code/sro_replication.py`: the analysis script; the other files in `code/` are the functions it uses (unchanged from the main study's repository). Run: `python3 code/sro_replication.py <Self_Regulation_Ontology/Data> OUT.json`. The script was tested only with `--synthetic` (all RTs replaced by random draws) before registration.
- `requirements.txt`: Python package versions.
- `SHA256SUMS.txt`: checksums of all files.

Data: Self-Regulation Ontology (Eisenberg et al., 2019; Enkavi et al., 2019), https://github.com/IanEisenberg/Self_Regulation_Ontology (commit 4e6e837fb5aaca87ed5914fd9be251156f43eec9), `Data/Complete_02-16-2019` and `Data/Retest_02-16-2019`, file `Individual_Measures/stop_signal.csv.gz`.
