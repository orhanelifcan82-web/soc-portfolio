# Case Study: Gloucester City Council Ransomware Attack (December 2021)

**Type:** Incident analysis / threat intelligence write-up
**Author:** Elifcan Orhan
**Skills shown:** incident analysis, attack timeline, MITRE ATT&CK mapping, threat actor attribution, lessons learned

> This write-up is based on public sources: the Local Government Association (LGA) case study *"Gloucester City Council: Managing a Cyber Attack"* (December 2023), the ICO's findings summarised in that report, and news reports. It is my own analysis for learning purposes.

---

## 1. Summary

In December 2021, Gloucester City Council in England was hit by a ransomware attack. The attack started with a **spear phishing email** sent through a **compromised supplier**. The attackers stayed hidden in the network for about a month, stole around **240,000 files**, and then encrypted the council's servers over a weekend just before Christmas.

The council did not pay the ransom. It recovered using secure backups, but full recovery took about **two years** and cost **over £1 million**. The attack was later linked to the **Conti** ransomware group, and the UK's GCHQ said the hackers were highly likely linked to Russian intelligence services.

---

## 2. Timeline

| Date | Event |
|---|---|
| Mid-November 2021 | A housing officer is in a normal email conversation with a known supplier. Around the 10th message, a link arrives that looks like it is from the supplier. The supplier had already been hacked. The link gives an error, so the officer thinks nothing of it, but malware is installed on the laptop. |
| A few weeks later | The laptop needs remote IT support for an unrelated problem. This gives the attackers a chance to spread across the network. |
| ~1 month (dwell time) | The attackers move through the network, gain control of the domain controller and steal data. |
| 18–19 December 2021 (weekend) | Ransomware is launched. About 240,000 files are sent to a file-sharing site in New Zealand. Staff who cannot log in think IT is doing maintenance. |
| 20 December 2021 | The incident is detected. Someone has to physically unplug cables in the data centre because the domain controller was compromised. Action Fraud is contacted. |
| 21 December 2021 | NCSC and NCA get involved and set up secure communication channels. |
| 22 December 2021 | The ICO is notified of the data breach. Partners are informed and a press statement is released. |
| 2022–2023 | New systems are built, around 70% of services move to the cloud, and data is restored. |
| August 2023 | The ICO issues a reprimand to the council. |

---

## 3. MITRE ATT&CK Mapping

My mapping, based on the steps described in public sources:

| Tactic | Technique | How it was used |
|---|---|---|
| Initial Access | T1199 Trusted Relationship | The attackers used a compromised supplier's email account. |
| Initial Access | T1566.002 Spearphishing Link | A malicious link was added to a real email conversation (thread hijacking). |
| Execution | T1204.001 User Execution: Malicious Link | The officer clicked the link. |
| Lateral Movement | T1021 Remote Services | The attackers spread across the network after a remote support session. |
| Privilege Escalation / Persistence | T1078 Valid Accounts | The attackers gained high-level access, including the domain controller. |
| Exfiltration | T1567.002 Exfiltration to Cloud Storage | About 240,000 files were sent to a file-sharing site in New Zealand. |
| Impact | T1486 Data Encrypted for Impact | Servers were encrypted with ransomware. |

---

## 4. Threat Actor

- **Group:** Conti, a Russian-speaking ransomware-as-a-service group (now disbanded).
- **Motivation:** Financial (ransom and double extortion), but the UK government said the group was highly likely linked to Russian intelligence. This shows that the line between cyber criminals and state-backed attackers can be blurred.
- **What happened to them:** In 2023, the UK and US sanctioned and charged several Russian members of the Conti/TrickBot group. Most have not been arrested, because Russia does not extradite its citizens. After the group shut down, former members are believed to have joined other ransomware groups.

### Could the ransom be a smokescreen?
Because of the possible links to Russian intelligence, I wondered if the ransom demand could hide another goal. This happened in the NotPetya attack (2017), which looked like ransomware but was actually designed to destroy data. In Gloucester's case there is no clear evidence of this, because the backups worked and the data was not destroyed. However, it is an interesting question for threat intelligence: a group linked to a state could make money from a ransom and, at the same time, serve state goals by disrupting public services or collecting data.

### Was it a planned attack?
Yes. The attackers waited for the right moment in a real conversation, stayed hidden for a month, stole data before encrypting it and launched the attack when nobody was watching. However, this was not a one-off "genius" plan. It followed a standard ransomware playbook used against many organisations. Because attacks follow patterns, they can be detected with the right monitoring.

---

## 5. Impact

- Services disrupted for **days to months**: housing benefits, planning applications, land searches and the electoral roll.
- About **21,000 postal voters** had to register again.
- Shared-service partners **blocked email** from the council, which made payroll, HR and legal work harder.
- Staff dealt with backlogs of up to **six months** and became fatigued.
- **Cost:** over £1 million (consultants, new hardware and cloud migration).
- **Regulatory:** reprimand from the ICO.

---

## 6. What Helped the Council Recover

1. **Secure backups** were stored separately, so the attackers could not reach them, and the council did not need to pay the ransom.
2. **Cloud services** (Microsoft 365, Teams and email) were not affected, so staff could still communicate and use workarounds.
3. **NCSC and NCA support:** secure communication channels, expert consultants and advice not to pay or contact the attackers.
4. **Other councils** that had been attacked before shared their experience.
5. **Clear priorities:** benefit payments were restored first so residents were not left without money over Christmas.

---

## 7. What Went Wrong (Root Causes)

- **No SIEM or central logging**, so a month of attacker activity was not detected. This was the ICO's main criticism.
- **No network segmentation**, so the attackers could move freely between servers.
- **Supply chain risk:** the attack came through a trusted supplier.
- **The user did not report the broken link.** It seemed normal, so it was never checked.
- **Business continuity plans were too general.** They planned for one system failing, not for losing all IT.
- **Heavily customised applications** were hard to restore from backups.

---

## 8. Lessons Learned

| Area | Lesson |
|---|---|
| Detection | Use a SIEM and central logging to spot attackers during the dwell time, before the ransomware stage. |
| Network | Segment the network so one compromised device cannot reach everything. |
| Supply chain | Check suppliers' security during procurement and monitor supplier risk. |
| Staff awareness | Training is not enough on its own. Encourage staff to report anything unusual, even a link that "just didn't work". |
| Planning | Have a specific cyber incident response plan and plan for the worst case. |
| Recovery | Keep offline backups, test restores regularly and document system configurations. |
| Mindset | It is "not if, but when". Prepare to respond and recover, not only to prevent. |

---

## 9. My Reflection

What I found most interesting was how the attack started. The employee was not careless. They were having a normal conversation with a supplier they knew, and they had done cyber security training. This showed me that the supply chain can be the weakest link, and that training alone cannot stop a well-prepared attacker.

I was also surprised by the one-month dwell time. It made me understand why SOC monitoring is so important: the best chance to stop a ransomware attack is during the quiet weeks before the encryption, when attackers are moving around the network.

---

## Sources

- Local Government Association (2023) *Gloucester City Council: Managing a Cyber Attack – Case Study*
- Hello Rayo (2023) *Russian hackers behind "sophisticated cyber-attack" on Gloucester City Council*: https://hellorayo.co.uk/greatest-hits/gloucestershire/news/russian-hackers-behind-sophisticated-cyber-attack-on-gloucester-city-council
- Digital Watch (2023) *Hackers behind Gloucester City Council cyberattack 'highly likely' linked to Russian intelligence services, GCHQ claims*: https://dig.watch/?p=136357
- National Crime Agency via Wired-Gov (2023) *Russian ransomware group hit with new sanctions*: https://wired-gov.net/wg/news.nsf/print/Russian+ransomware+group+hit+with+new+sanctions+11092023111500
- BleepingComputer (2023) *US and UK sanction TrickBot and Conti ransomware operation members*: https://www.bleepingcomputer.com/news/security/us-and-uk-sanction-trickbot-and-conti-ransomware-operation-members/
- MITRE ATT&CK: https://attack.mitre.org/
