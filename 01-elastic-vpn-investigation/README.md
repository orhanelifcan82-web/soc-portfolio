# 01 – VPN Failed Login Investigation (Elastic Stack / Kibana)

**Source:** TryHackMe, *Elastic Stack: The Basics* (SOC Level 1 path, Core SOC Solutions module)
**Tools:** Kibana Discover, KQL, Kibana Lens visualisations, dashboards
**Role played:** Level 1 SOC Analyst

> Room answers and flags are intentionally not included. This write-up focuses on methodology.

## 1. Scenario

The SOC received VPN connection logs for a company and needed to check for suspicious activity.
My task was to find **failed VPN connection attempts**: which users they came from and which
source IP addresses were involved. Repeated failed logins can be an early sign of password
guessing or a brute-force attack.

## 2. Investigation steps

### Step 1: Select the right data
In Kibana Discover I selected the `vpn_connections` data view, so that I was only looking at
VPN logs.

### Step 2: Set the correct time range
Kibana shows only the last 15 minutes by default, so no events appeared at first. I used the
time picker to set an **absolute** time range covering **January 2022**, when the logs were recorded:

```
Start: Jan 1, 2022 @ 00:00:00.000
End:   Jan 31, 2022 @ 23:59:59.999
```

**Lesson:** a wrong time range is one of the most common reasons an investigation "finds nothing".

### Step 3: Filter for failed attempts
I filtered the events to show **only** failed connections, using KQL in the search bar:

```kql
action : failed
```

I made sure to use an **include** filter (`is`), not an exclude filter (`is not`). Excluding
failed events would have hidden exactly the activity I was investigating.

### Step 4: Find the users with the most failed attempts
I opened the `UserName` field in the field list. Kibana showed the most frequent values and their
percentages for the filtered events, so I could see straight away which user had the most failed attempts.

### Step 5: Build a visualisation
To summarise the findings, I created a **table visualisation** in Kibana Lens:

| Setting | Value |
|---------|-------|
| Rows | `UserName`, `Source_ip` |
| Metric | Count of records |
| Sort | Count, descending |

The table shows **who** failed to connect, **from where**, and **how many times**. I saved it to a
dashboard so it could be reused.

![Failed VPN attempts table](screenshots/failed-attempts-table.png)
<!-- Add your own screenshot: save it as screenshots/failed-attempts-table.png -->

## 3. Analyst assessment

<!-- Write this section in your own words. Example questions to answer:
- Was one user or one IP responsible for most of the failures?
- Did the attempts happen in a short burst or spread over time?
- Is the IP internal or external? Is it unusual for that user?
-->

If a single user or IP is responsible for a high number of failed attempts in a short period,
I would treat it as a **possible brute-force or password-guessing attempt**. As an L1 analyst I would:

1. Check whether any **successful** login followed the failed attempts from the same IP (`action : success`).
2. Enrich the source IP with a threat intelligence lookup (for example, check its reputation).
3. Check whether the user account is valid, disabled or recently changed.
4. **Escalate** to Tier 2 if a successful login followed the failures or the IP is malicious;
   otherwise document the activity and recommend account lockout or MFA review.

## 4. What I learned

- How to scope an investigation with the right **data view** and **time range**
- How to write simple **KQL** filters and avoid include/exclude mistakes
- How to use field statistics to find top values quickly
- How to turn raw logs into a **visualisation and dashboard** that others can read
- How to think beyond the answer: **what would I do next as an analyst?**
