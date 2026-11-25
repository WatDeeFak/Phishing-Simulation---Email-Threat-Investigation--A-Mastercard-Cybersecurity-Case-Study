# Evidence Register and Methodology

> All evidence is fictional training data. This register documents what was observed in the case scenario and what cannot be inferred from it.

## Methodology

1. **Triage:** inspect sender, recipient, subject, body, attachment names, and headers.
2. **Authentication:** evaluate SPF, DKIM, DMARC, and domain alignment.
3. **URL review:** distinguish display text, initial destination, redirect parameters, and final destination.
4. **Attachment triage:** inspect extension, file signature, hash reputation, and sandbox observations without executing the sample on a production endpoint.
5. **Correlation:** connect artefacts by domain, identifier, timestamp, and observed behavior; keep unrelated evidence separate unless supported.
6. **Impact review:** compare click telemetry with endpoint and identity logs.

## Important interpretation rules

- A PASS result is scoped to the mechanism being evaluated; it is not a verdict that the email is safe.
- A different Reply-To or Return-Path domain is an indicator to verify, not proof by itself.
- A redirect parameter is not proof of an open-redirect vulnerability.
- A new domain or low-prevalence URL is not automatically malicious.
- File extensions can be misleading; file signatures help identify format but do not establish safety.
- A sandbox report describes behavior in the sandbox, not on the employee's endpoint.
- A click event does not establish credential submission.

## Evidence matrix

| ID | Source | Observation | Assessment | Limitation |
|---|---|---|---|---|
| E-01 | Email header | External Reply-To: `reward-claims@example.net` | Suspicious sender/reply mismatch | Vendor authorization not verified |
| E-02 | Email authentication | SPF PASS; DKIM PASS; DMARC FAIL | Both authenticated domains fail alignment with visible From | Does not alone establish malicious content |
| E-03 | Received / Return-Path / Message-ID | Shared `rewards-notice.example.net` domain family | Infrastructure correlation | Does not identify actor or ownership |
| E-04 | HTML hyperlink | Display text differs from actual destination | Link masking / mismatch | Requires safe static inspection; no live click required |
| E-05 | Redirect parameter | Target is `login-rewards.example.org` | External destination to inspect | Parameter alone does not prove a redirect vulnerability |
| E-06 | Landing page | Microsoft 365 lookalike requests credentials | Strong credential-harvesting indicator | No submission evidence |
| E-07 | URL reputation | Initial 3/90; target 18/90 | Supporting threat-intelligence evidence | Simulated counts; vendor ratios are not a severity score |
| E-08 | Attachment metadata | `.pdf.exe`; `4D 5A` signature | Executable candidate disguised as document | File type does not equal maliciousness |
| E-09 | File reputation | 31/70 simulated detections | Supports likely-malicious assessment | Reputation is not a standalone verdict |
| E-10 | Sandbox | PowerShell, DNS/HTTP, file creation, Run-key modification | Suspicious sample behavior | Not proof of endpoint execution |
| E-11 | Email gateway | 24 delivered; 3 unique URL clicks | 12.5% simulated click rate | Does not prove credential submission or execution |
| E-12 | EDR | No matching execution event in scoped search | No execution observed in that scope | Coverage and time window are limited |
| E-13 | Identity provider | No confirmed suspicious successful sign-in | Account takeover not established | Does not rule out every exposure scenario |

## Evidence provenance

All observations above were authored as synthetic exercise data for a portfolio case study. They are not sourced from a real production system. The purpose is to practice evidence handling and reasoning, not to claim forensic access to Mastercard infrastructure.
