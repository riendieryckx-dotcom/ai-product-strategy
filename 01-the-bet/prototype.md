# The Prototype Bet

## What I Built
A one-screen view where a care path team selects a hip fracture patient profile and sees comparable past stays in a synthetic hospital: which care path variants were used and in what share, with length of stay, 30-day readmissions, cohort size, uncertainty ranges, the patient mix per care path, and an AI-written summary for the committee that explains selection effects instead of recommending a treatment.

## Tool Used
Claude (claude.ai published artifact, live AI via Claude, with a rule-based fallback)

## Prototype Link
https://claude.ai/artifact/N33V65z3Lei41zDHjyqMuA

## AI Value Archetype
Oracle — it surfaces patterns hidden in the records of all hospitals on the network; people decide what to do with them.

## The Bet in One Sentence
Care path committees, and later physicians, in hospitals on our EHR will use a view of how comparable patients in their own hospital and across the network were treated and what happened next, because the EHR already captures every treatment and outcome across many hospitals, and AI now makes it feasible to find truly comparable patients in that pooled data, which no single hospital or general health model can see.

## Kill Criteria
Pilot with hospitals on the network, 6 months, one care path (hip fracture). Stop if:

- fewer than 3 hospitals agree to pool pseudonymised data within 6 months;
- legal and DPO review finds no workable legal basis for pooled secondary use;
- clinical reviewers judge more than a quarter of the displayed "comparable" patients as not comparable;
- no participating care path committee uses the view to start at least one care path discussion.
