# The Prototype Bet

## What I Built
A screen where a physician opens a synthetic patient on an internal medicine ward with an unclear diagnostic workup. It shows the findings from the patient's history that fit the current picture and are not yet in the current notes, each with its source and the reason it was selected. Above them, it shows up to five possible diagnoses, each with an ICD-10 code, a likelihood label, the estimated chance of major or extreme severity if confirmed, and links to the supporting findings. When a new lab result arrives, both lists update and show what changed. The physician marks each finding and suggestion; nothing is applied automatically. The page rejects AI output that refers to findings not in the record.

## Tool Used
Claude (published claude.ai artifact, live AI via Claude, with a scripted fallback)

## Prototype Link
https://claude.ai/artifact/NYFskdj1szmhGDcKuRVgWQ

## AI Value Archetype
Copilot — the physician keeps the diagnosis; the AI keeps the differential current with the record, shows its evidence and estimates severity.

## The Bet in One Sentence
Hospital physicians on our EHR will use a certified module that suggests possible diagnoses with an estimated severity, grounded in findings from the patient's own history and updated with every new result, because the EHR already holds the full record and every confirmed outcome, AI can now reason over it in real time, and a general model cannot be used officially for this in a European hospital until it is certified.

## Kill Criteria
Retrospective test on pseudonymised data from 2 hospitals, then a supervised pilot in which physicians see the module on 2 internal medicine wards, 6 months. Stop if:

- the confirmed discharge diagnosis is in the top 5 suggestions in a lower share of stays than a list based on how common each diagnosis is for the same complaint;
- for stays that reached severity 3–4, the severity percentage does not separate them from other stays better than the admission data alone;
- clinical reviewers judge fewer than 2 in 3 shown history findings as relevant to the case;
- after month 2 of the pilot, physicians open the module in fewer than half of the eligible stays;
- the regulatory assessment shows no path to first clinical use within 36 months, or certification costs above the budget set in Module 3;
- the legal and DPO review finds no workable basis to use confirmed outcomes and physicians' marks to calibrate the model.
