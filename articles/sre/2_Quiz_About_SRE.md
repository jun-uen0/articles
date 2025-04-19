## SRE QUIZ #1: SLA/SLO/Error Budget

### Problem
Your API service has a 99.95% monthly SLO. During one month, there are two incidents:
- Incident A: 1.5-hour outage with 503 errors
- Incident B: 30-minute latency spike above the 95th percentile

### Question
Is your SLO violated this month? Justify using math and the concept of error budgets.

### Answer
Yes. 99.95% monthly SLO allows ~22 minutes of downtime. Incident A alone (90 minutes) violates the SLO. Incident B depends on whether the SLO includes latency objectives — if it does, then it's also a violation. Error budget is exhausted.

---

## SRE QUIZ #2: Incident Response

### Problem
A 2:00 AM alert says 5xx error rate > 10% for `api-gateway`. Frontend is timing out. New `catalog-service` deployed 30 minutes prior.

### Question
What are your first 3 steps as incident commander? Don’t fix the bug — focus on reliability actions.

### Answer
1. Acknowledge and triage the alert to prevent duplicate escalations
2. Mitigate impact (e.g. rollback `catalog-service`, shift traffic)
3. Communicate status (Slack, status page, page catalog owner)

---

## SRE QUIZ #3: Toil Reduction

### Problem
You manually terminate zombie EC2s from failed CI/CD runs each week. It takes hours.

### Question
How would you eliminate this toil using SRE principles?

### Answer
- Short term: Write a termination script
- Long term: Automate cleanup with cronjob or Lambda
- Bonus: Add TTL tags to CI-created instances for easier future integrations

---

## SRE QUIZ #4: Capacity Planning

### Problem
Traffic expected to spike from 120 RPS to 400 RPS during a marketing campaign. Backend throttles at 200 RPS.

### Question
How do you prepare?

### Answer
- Review past load campaign metrics (CPU, DB, errors)
- Enable and tune auto-scaling thresholds
- Add queueing layer if needed (SQS, Pub/Sub)
- Run load tests beforehand
- Add campaign-specific dashboards
- Confirm rollback or scale-down options

---

## SRE QUIZ #5: RCA (Root Cause Analysis)

### Problem
Uploads failed for 45 minutes due to proxy misconfig. Fixed, but reoccurred next day via staging config promotion.

### Question
What action items prevent recurrence?

### Answer
- Add config validation step in CI/CD pipeline
- Document proxy config ownership and change process
- Share postmortem widely with dev team
- Add alerting for API latency spikes

---

## SRE QUIZ #6: Toil

### Problem
You manually rotate 10+ API keys for third-party integrations with different formats and schedules.

### Question
What’s your short-term and long-term strategy to eliminate this toil?

### Answer
- Short-term: Write scripts to rotate keys
- Long-term: Automate with scheduled serverless jobs
- Bonus: Make reusable templates for future integrations

---

## SRE QUIZ #7: Resilience / Chaos Engineering

### Problem
Your app runs across 3 AZs. You want to test resilience against an AZ failure.

### Question
Describe an experiment to validate the system survives AZ failure. What would you break, observe, and do if the system degrades?

### Answer
- Break: Stop EC2s in AZ-a or deregister them from ALB
- Observe: ALB health checks, error rates, RPS, app behavior
- If degraded: Abort experiment, restore EC2s or targets, analyze cause (e.g., sticky sessions, AZ-pinned DB)

---

## SRE QUIZ #8: Monitoring & SLO Alerts

### Problem
Your 99.9% SLO was violated by a 2-hour 5xx rate of 2%. Your alert was set to trigger at >10% for 1 minute, so it never fired.

### Question
Why didn’t your alert catch this?
How would you redesign your alerting system to protect the SLO?

### Answer
- Alert was tuned for outages, not slow-burns
- New thresholds:
  - Medium: >0.05% per 1 min
  - Warning: >0.075%
  - Error: >0.9%
  - Critical: >10%
- Bonus: Use burn rate alerting to trigger when you're consuming error budget too fast

---

## Summary
| Quiz | Topic                     | Summary                                                       |
|------|---------------------------|---------------------------------------------------------------|
| 1    | SLA/SLO/Error Budget      | Misjudged long-running small errors can burn error budgets   |
| 2    | Incident Response         | Focus on mitigation, not root cause during active incidents   |
| 3    | Toil Reduction            | Eliminate repetitive tasks with automation and abstraction    |
| 4    | Capacity Planning         | Use historical data + pre-load test + autoscaling             |
| 5    | RCA                       | Prevent recurrence with config controls + postmortem sharing  |
| 6    | API Key Rotation (Toil)   | Automate with cron/serverless + reusable template             |
| 7    | Chaos / Resilience        | Simulate AZ failure + observe impact + restore quickly        |
| 8    | Monitoring / SLO Alerts   | Tune alerts to match burn rate, not just spike detection      |
