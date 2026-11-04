# The Prototype Bet

## What I Built
A screen with a synthetic patient on an internal medicine ward: history findings that fit the current picture, each with its source, and up to five diagnosis suggestions with an ICD-10 code, a likelihood label and a severity percentage. A new lab result updates both lists and shows what changed. The physician marks each item; nothing is applied automatically, and AI output that cites a finding not in the record is rejected. The prototype shows a stay; the outpatient flow (preparing a consultation, results arriving between visits) is not in it yet.

## Tool Used
Claude (published claude.ai artifact, live AI with a scripted fallback)

## Prototype Link
https://claude.ai/artifact/NYFskdj1szmhGDcKuRVgWQ

## AI Value Archetype
Copilot — the physician keeps the diagnosis; the AI keeps the differential current, shows its evidence and estimates severity.

## The Bet in One Sentence
Hospital physicians on our EHR will use a certified module that suggests possible diagnoses with an estimated severity, grounded in the patient's own history and updated with every new result, during a stay or an outpatient workup, because the EHR already holds the full record and every confirmed outcome, AI can now reason over it in real time, and a general model may not be used for this in a European hospital until it is certified.

## Kill Criteria
Retrospective test in 2 hospitals, then a 6-month supervised pilot on 2 wards and their outpatient clinics. Stop if:

- the top 5 is no better than a list based on how common each diagnosis is (top 1 reported separately);
- physicians with the module do not reach the confirmed diagnosis more often or sooner than before go-live;
- tests per stay or outpatient workup rise by more than 10% without better outcomes;
- the severity percentage separates serious courses no better than the data at the start of the stay or workup;
- fewer than 2 in 3 history findings are judged relevant;
- after month 2, the module is opened in fewer than half of eligible stays and consultations;
- there is no path to clinical use within 36 months, or certification exceeds the Module 3 budget;
- there is no legal basis to use outcomes and physicians' marks for calibration.
