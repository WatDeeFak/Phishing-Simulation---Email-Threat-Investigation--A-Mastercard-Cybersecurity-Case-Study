# Phishing Awareness Campaign Design and Metrics

> This is a proposed design and a worked example using fictional data. No real employees were targeted and no campaign telemetry was collected.

## Campaign objective

Teach employees to recognize common phishing indicators and use the organization's reporting process. The exercise should measure safe learning outcomes without collecting real passwords or deploying malware.

## Safe simulation principles

- Obtain written authorization and define the audience, timing, and scope.
- Use a domain and landing page controlled by the exercise owner and approved by security, legal, and privacy stakeholders.
- Use a harmless landing page that records only approved interaction telemetry.
- Never collect real passwords, MFA codes, session cookies, or sensitive personal information.
- Never attach or distribute a live executable or malicious payload.
- Provide a clear debrief and training after the exercise.
- Limit access and retention of user-level telemetry.

## Fictional scenario dataset

| Metric | Simulated value | Interpretation |
|---|---:|---|
| Emails delivered | 24 | Scenario denominator |
| Unique link clicks | 3 | Simulated click events |
| Click rate | 12.5% | 3 / 24 × 100 |
| Confirmed credential submissions | Unknown | No evidence supplied |
| Attachment executions | Unknown | No employee execution evidence supplied |
| Confirmed account takeovers | 0 established | Not established by the scenario evidence |

The 12.5% value is a calculation over a fictional case dataset. It is not a real campaign result, benchmark, or employee susceptibility score.

## Useful campaign metrics

- **Delivery rate:** delivered messages / attempted messages × 100.
- **Unique click rate:** unique users who clicked / delivered messages × 100.
- **Report rate:** unique users who reported the message / delivered messages × 100.
- **Credential submission rate:** simulated submissions / delivered messages × 100. Use only a harmless training event; never collect actual passwords.
- **Attachment execution rate:** users who executed a safe simulator / delivered messages × 100. Do not use real malware.

Define numerator, denominator, deduplication rules, tracking scope, and privacy controls before measuring any rate. A click is not proof of credential submission, and a low click rate alone does not prove that employees can identify all phishing attempts.

## Training recommendations

1. Explain urgency, fear, reward, and authority-based social engineering.
2. Teach employees to inspect actual link destinations and use official bookmarks or known portals.
3. Teach safe handling of unexpected attachments and double extensions.
4. Encourage prompt reporting through the approved phishing-report button or service desk.
5. Provide a short, non-punitive debrief focused on learning.
