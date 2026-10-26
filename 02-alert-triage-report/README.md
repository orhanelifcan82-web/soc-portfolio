# 02 – L1 Alert Triage Report (Template + Example)

A Level 1 SOC analyst's job is to quickly decide whether an alert is a **true positive** or a
**false positive**, and whether it needs **escalation**. Clear reporting matters because Tier 2
analysts rely on L1 notes to continue the investigation.

This is the report structure I use, based on what I learned in the TryHackMe *SOC L1 Alert Triage*
and *SOC L1 Alert Reporting* rooms.

---

## Report template

| Field | Details |
|-------|---------|
| **Alert name** | |
| **Alert ID / time** | |
| **Severity** | Low / Medium / High / Critical |
| **Affected user / host** | |
| **Source (IP / domain / file)** | |
| **Data sources checked** | e.g. SIEM logs, EDR, VPN logs, email gateway |

### Summary
*One or two sentences: what happened?*

### Investigation steps
1.
2.
3.

### Findings / evidence
-

### Verdict
- [ ] True positive
- [ ] False positive
- [ ] Needs more information

### Action taken
- [ ] Escalated to Tier 2 (reason: )
- [ ] Closed (reason: )
- [ ] Recommended remediation:

---

## Example (based on my VPN investigation, lab 01)

| Field | Details |
|-------|---------|
| **Alert name** | Multiple failed VPN logins |
| **Severity** | Medium |
| **Affected user / host** | *[user from the investigation]* |
| **Source (IP / domain / file)** | *[source IP from the investigation]* |
| **Data sources checked** | VPN connection logs (Elastic / Kibana) |

**Summary:** One user account had a much higher number of failed VPN connection attempts than
other users during January 2022.

**Investigation steps:**
1. Filtered VPN logs for `action : failed` over the alert time range.
2. Grouped the results by `UserName` and `Source_ip` to find the main source of failures.
3. Checked for successful logins from the same IP after the failed attempts.

**Verdict:** *[Your decision]*

**Action taken:** *[Escalate or close, with a one-line reason]*
