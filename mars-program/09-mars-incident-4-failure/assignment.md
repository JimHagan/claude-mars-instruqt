---
slug: mars-incident-4-failure
id: 1hpiyuerfoi7
type: challenge
title: 'Incident 4: Failure'
teaser: Some orders are going through, some aren't
tabs:
- id: txdrnbxnjvtm
  title: Check
  type: terminal
  hostname: k8s
  cmd: /tmp/generic_prompt
- id: pasimdme17il
  title: Astronomy Shop
  type: service
  hostname: k8s
  path: /
  port: 30080
difficulty: ""
timelimit: 1800
enhanced_loading: null
---

# 🚨 Incident Alert: Intermittent Payment Failures

**Severity:** P1 — Revenue Impact
**Impact:** A percentage of payment charges are failing — affected customers cannot complete purchases

Your team is paged. New Relic is showing errors in the payment flow, but they're **not 100% failures** — some transactions are succeeding while others fail.
This is trickier than a total outage. Customers are having inconsistent experiences and support tickets are piling up.

## 🎯 Your Mission

Use New Relic to investigate and identify:

1. **What is the name of the service** that is intermittently failing?
2. **What is the approximate error rate** observed in APM?
3. **What is the name of the failing transaction?**

## 🔍 Investigation Guide

Start broad, then narrow down.  As always check your configured workloads to get awareness of impacted entities:


### Step 1: A Little About Alerts

In a real environment you may receive a page related to an alert in New Relic.  This is often the first thing you'll look at as you may not even be in front of your computer.  From that brief glance you may be able to see what service or services are impacted and what the general issue is: `high error rate`, `high latency` etc. 

When an alert fires to create an incident it may be associated with one or more service.   When you see a service in the entities overview or in a workload the color of that alert will be red if it's assocated with an open alert incident.

For our exercise let's shart with our workload.

### Step 2: Review Your Workload 

Look at your workload.  You'll see that one or more of the services are showing `red`.  This means there are active alerts on those servies.  You may click on the icons for those services to see the incident summary.  Since `checkout` is the common starting point for payment processing you may see that it is currently impacted.

However let's try to find the `downstream` cause of it's current state.

### Step 1: Dig into APM
1. Go to **APM & Services**
2. Click into the `checkout` service and examine:
   - The **Errors** Inbox — look at the error messages and stack traces
   - **Distributed Tracing** — find traces with errors and examine the failing span
   - Find out which **downstream** service is throwing an error.
   - View the APM summary for **that** downstream service.
   - Use the APM summary page to evaluate the error rate for that service.

### Step 3: Find The Exact Span Name Related to The Error Spike
1. There are a number of places to find this information, however the trusty *APM* home page is a good starting point.  The left navigation panel in APM provides all the features you'll need (actuallly much more).
2. For a real savvy power user you could probably identify this with a customer NRQL query although it's not necessary.
2. Some span names will have simple mnemonic names others will be a little more cryptic.


## 📝 Submit Your Answers

Once you've identified the root cause, go to the **Check** terminal and enter your answers:

**Answer Format:**

```
failing service; approximate error rate; failing transaction name
```

**Example:** `frontend; 5%; processItem`

**Format hints:**
- Failing service: use the exact name as it appears in New Relic APM (e.g., `frontend`)
- Approximate error rate: observe the error rate in APM and round to the nearest 5% (e.g., `5%`)
- Failing transaction name: This is the exact text of the spans `name` attribute (e.g., `processItem`)

Click the **Check** button to validate. You can re-enter if incorrect.

## ⏱️ Notes

- You have **15 minutes** for this incident
- If stuck after 10 minutes, ask your Game Manager for a hint
- Your SLO burn rate is ticking — move fast! 🚀
 — try at least 5 times."

- The error rate fluctuates over time. A student who checks APM in a
  "lucky" window may see a lower rate than the configured ~25%. The check
  script needs to accept a range (e.g., 15%–35%) not just "25%".

- Students who did Incident 2 will recognize "paymentservice" immediately
  and may jump straight to that service — which is actually correct here!
  But the reason is different (internal error vs. connection refused).
  Watch for teams who get the right answer for the wrong reason and then
  struggle to explain WHY in a debrief.

- The transaction name ("ChargeRequest", "Charge", etc.) may differ
  between the OTel span name and the APM transaction name. Verify the
  exact string that appears in APM before the beta and ensure the check
  script matches it exactly. Also handle case variants.

- Teams fatigued from Incidents 1–3 may rush this one and miss the
  "intermittent" nuance. This is arguably the most analytically
  challenging incident — game managers should be ready to slow teams
  down and prompt reflection.
=============================================================================
-->
