# Incident Response Plan: LEA Biotech Ltd

**Type:** Incident response planning
**Author:** Elifcan Orhan
**Skills shown:** incident response lifecycle, incident classification and escalation, roles and responsibilities, UK GDPR/ICO reporting, access control, communication planning

> LEA Biotech Ltd is a fictional organisation that I created to practise writing a cyber security incident response plan. It was developed as part of my NCFE Level 3 Certificate in Cyber Security Practices.

---

## 1. Organisation and Scope

LEA Biotech Ltd is a vaccine research company based in Kent. It has around 150 employees and a small IT team with five people. The company is working on a universal flu vaccine. It also runs clinical trials and makes small amounts of vaccines for testing. Large-scale production is done by another company.

This plan covers all employees, contractors and suppliers. It also protects important company assets, such as vaccine research data, clinical trial data, cold storage systems and laboratory systems.

The main threats are ransomware, phishing, insider threats and attacks on cold storage systems.

---

## 2. Purpose of the Plan

LEA Biotech works on important vaccine research, so it could be a target for cyber criminals. The purpose of this plan is to help the company prepare for cyber attacks and deal with them as quickly as possible.

It aims to protect research data and clinical trial participants' personal and health information, and keep vaccines safe. It also helps the company avoid financial losses and follow the law. For example, under UK GDPR, some personal data breaches must be reported to the ICO within 72 hours.

---

## 3. Roles and Responsibilities

| Role | Responsibility |
|---|---|
| IT Manager (Incident Coordinator) | Leads the response and makes important decisions. |
| Security Analyst | Receives reports, checks what happened and collects evidence. |
| Systems Administrator | Disconnects affected systems and restores them from backups. |
| IT Support Technicians (x2) | Help employees, check computers and reset passwords. |
| Lab Operations Manager | Protects the laboratory and cold storage systems, and moves vaccines to another safe place if needed. |
| Data Protection Officer (external) | Checks if a data breach needs to be reported to the ICO. |
| HR Manager | Deals with cases where employees misuse their access. |
| Managing Director | Makes important decisions and communicates with partners and the media. |
| External Security Provider | Gives extra technical help because the company has a small IT team. |

---

## 4. How an Incident is Reported and Logged

Employees must report anything suspicious to the IT team as soon as possible. Examples include a phishing email, a ransom message, an employee copying a lot of research data or an unusual change in freezer temperatures. Employees should not try to fix the problem themselves or turn off affected computers.

The Security Analyst records the incident in an incident log. The log includes the date, time, what happened, who reported it and which systems are affected. It is also updated during the incident and can be used as evidence.

---

## 5. Classification

Incidents are classified by two things: **severity** and **impact**. There are three priority levels.

| Priority | Response time | Examples |
|---|---|---|
| **High** | Immediately | Ransomware affecting research servers, an attack that changes freezer temperatures, stolen clinical trial data, or an employee stealing the vaccine formula. |
| **Medium** | Within 1 hour | Malware found on one laptop, or an employee clicking a phishing link and entering their password. |
| **Low** | Within 24 hours | An employee reports a phishing email but does not open it. |

If the situation becomes worse, the priority is increased and the incident is escalated again.

---

## 6. Response Steps

The company follows the stages of the Incident Response Lifecycle.

**Preparation:** The company keeps offline backups, uses MFA and keeps the cold storage systems separate from the main network. It also uses access control, so employees can only access the data they need for their job. This is called least privilege. Access to the vaccine formula and research data is monitored, USB drives are restricted, and access is removed immediately when an employee leaves the company.

**Detection and Analysis:** The Security Analyst checks security alerts, logs, temperature alarms and reports from employees. This helps them find out what happened and decide the priority.

**Containment:** The team disconnects affected systems and disables accounts that may be compromised, including the account of an employee suspected of an insider threat. If the freezers are at risk, vaccines are moved to backup storage.

**Eradication:** The team removes malware, fixes security problems by installing patches and resets passwords.

**Recovery:** The company restores systems using clean backups. The cold storage monitoring system is restored first because keeping vaccines at the correct temperature is very important. After this, the systems are checked regularly.

---

## 7. Communication

**Internal communication:** The IT Manager keeps the Managing Director and the response team updated. They use a secure way to communicate, such as phone calls, because email may be affected by the attack. Employees are also given clear instructions. For example, they may be told not to open certain emails or use affected systems.

**External communication:** The DPO checks if a personal data breach needs to be reported to the ICO within 72 hours. If clinical trial participants are at risk, they may also need to be informed. The Managing Director contacts research partners and the company that does the large-scale manufacturing. The company also reports cyber crimes to the police and NCSC. Any problems that could affect vaccine safety are reported to the MHRA.

---

## 8. Review and Improvement

After every incident, the team holds a lessons learned meeting. They discuss what happened, what went well and what could be done better next time. The company then writes an incident report and makes changes to the plan, security controls and staff training.

The plan is tested at least once a year with the external security provider. For example, the team can practise how to deal with a ransomware attack. The plan is also reviewed when the company gets new staff, new systems or has to follow new regulations.

---

## Incident Response Checklist

- [ ] Report the incident to the IT team immediately. Do not try to fix it yourself or turn off the computer.
- [ ] Record the incident in the incident log. Include the date, time, details and affected systems.
- [ ] Decide if the incident is high, medium or low priority and inform the correct people.
- [ ] Disconnect affected systems and disable compromised accounts to contain the incident.
- [ ] Check the freezer temperatures and move vaccines to backup storage if needed.
- [ ] Check if clinical trial data is affected. If necessary, report the breach to the ICO within 72 hours.
- [ ] Remove the threat and restore the systems using clean backups.
- [ ] Hold a lessons learned meeting and make improvements to the plan and staff training.
