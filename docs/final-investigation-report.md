# Final Investigation Report — MC-2026-001

> **Training-only report:** all entities, domains, logs, telemetry, hashes, and findings below are fictional. This is not a real Mastercard incident or employee investigation.

## 1. Executive summary

The simulated case concerns an employee-reward email that uses a reward lure and a 6 PM deadline to encourage interaction. The message contains an external hyperlink and an attachment named `Employee_Reward_Coupon.pdf.exe`.

The investigation identified a mismatch between the visible sender domain and the domains used by the Reply-To, Return-Path, and DKIM signing infrastructure. SPF and DKIM passed independently, but neither authenticated domain aligned with the visible From domain; DMARC therefore failed. The hyperlink led through an external redirect parameter to a Microsoft 365 lookalike page requesting an email address and password. The attachment was an executable candidate disguised with a double extension and produced suspicious behaviors in a simulated sandbox.

The email is assessed as a **phishing attempt (high confidence within the fictional scenario)**. The attachment is assessed as **likely malicious**. The available evidence does not establish credential submission, account takeover, or infection of an employee endpoint.

## 2. Scope and methodology

The fictional investigation reviewed:

- Email metadata and authentication results.
- Hyperlink text, actual destination, redirect parameter, and landing-page content.
- Attachment filename, file signature, SHA-256, reputation results, and sandbox observations.
- Email gateway, endpoint detection, and identity-provider findings supplied in the scenario.

No live URLs were visited and no executable was run on a user endpoint. The sandbox and telemetry results are simulated evidence.

## 3. Email analysis

### 3.1 Key header values

| Field | Simulated value |
|---|---|
| From | `rewards@mastercard.example` |
| To | `tika@mastercard.example` |
| Reply-To | `reward-claims@example.net` |
| Return-Path | `bounces@rewards-notice.example.net` |
| Message-ID | `<20261122.081500.7f3a@rewards-notice.example.net>` |
| Received | `mail.rewards-notice.example.net` (`198.51.100.24`) to `mx.mastercard.example` |

The external Reply-To differs from the visible sender domain. The Return-Path and Received hostname use `rewards-notice.example.net`, which also appears in the initial URL. This is an infrastructure correlation, not proof of actor identity or authorization status.

### 3.2 Authentication

| Mechanism | Result | Alignment interpretation |
|---|---|---|
| SPF | PASS | SMTP MAIL FROM domain `rewards-notice.example.net` did not align with From domain `mastercard.example` |
| DKIM | PASS | `d=rewards-notice.example.net` did not align with From domain `mastercard.example` |
| DMARC | FAIL | Neither SPF nor DKIM passed with the required alignment |

Authentication PASS does not mean the message is safe. DMARC alignment is evaluated against the visible From domain.

## 4. URL and landing-page analysis

- Display text: `View Your Employee Reward`.
- Initial URL host: `rewards-notice.example.net`.
- Redirect parameter target: `login-rewards.example.org`.
- Initial URL reputation: 3/90 simulated detections.
- Redirect target reputation: 18/90 simulated detections.
- Landing-page observation: Microsoft 365 branding on an external domain, requesting an email address and password.

The mismatched branding and credential request support a credential-harvesting assessment. No credential-submission record was provided. A `redirect` parameter alone does not establish an open-redirect vulnerability; application behavior and validation would need to be tested in an authorized environment.

## 5. Attachment analysis

| Attribute | Simulated finding |
|---|---|
| Filename | `Employee_Reward_Coupon.pdf.exe` |
| Reported MIME type | `application/octet-stream` |
| File signature | `4D 5A` (`MZ`, Windows PE candidate) |
| SHA-256 | `8f3a7c91d2e4b650a1c9f0275b6d83e49a2f1c7d8e5b4a603f9d2c1e7b5a8046` |
| Reputation | 31/70 simulated detections |
| Detection categories | 18 Trojan/Downloader, 7 generic malware, 6 suspicious |
| Previous filenames | `invoice.exe`, `employee_reward.exe` |

Sandbox observations included an executable spawning PowerShell, a DNS query for `cdn-update.example.org`, an HTTP connection to `198.51.100.75`, creation of `C:\Users\Public\update.tmp`, and a Registry Run Key persistence attempt. No confirmed credential-access behavior was observed in the sandbox.

These observations support a **likely malicious** assessment of the attachment. They do not establish execution on an employee endpoint.

## 6. Evidence correlation

The Return-Path, Message-ID, Received hostname, and initial URL share the registered domain `example.net`. The URL parameter `employee=tika` links the URL context to the intended recipient. The initial URL redirects by parameter to a separate `example.org` domain whose page imitates Microsoft 365 and requests credentials.

Separately, the attachment's filename and PE signature, reputation results, and sandbox behavior support a potential malware-delivery path. The sandbox network indicator `cdn-update.example.org` and the URL redirect target `login-rewards.example.org` share the registered domain `example.org` but use different subdomains. The scenario provides no evidence proving that the two services are related or share an operator.

### Observed facts

- 24 messages were delivered.
- Three unique URL clicks were recorded.
- The landing page displayed Microsoft 365 branding and requested credentials.
- Sandbox execution showed suspicious process, network, file, and Registry behavior.
- No matching attachment execution was found in the scoped managed-endpoint search.
- No confirmed successful suspicious sign-in or account takeover was established.

### Unknowns

- Whether any clicker submitted credentials.
- Whether the attachment was downloaded or executed by any employee.
- Whether unmanaged devices or log sources outside the defined scope were affected.
- Whether any data was exfiltrated.

## 7. Classification and impact assessment

| Object / impact | Assessment | Confidence / limitation |
|---|---|---|
| Email | Confirmed phishing attempt in the fictional scenario | High; supported by impersonation page and credential request, plus header and lure indicators |
| Attachment | Likely malicious | High suspicion; sandbox and reputation support this, but it is simulated evidence |
| Credential compromise | Not established | No submission evidence supplied |
| Account takeover | Not established | No confirmed unauthorized successful sign-in supplied |
| Endpoint infection | Not established | No matching execution event found in the stated managed-endpoint scope |

The scenario's click rate is 3/24 = 12.5%. This is a fictional scenario metric, not a real employee campaign result.

## 8. Incident-response recommendations

1. Preserve the original `.eml`, headers, attachment, hashes, and collection metadata.
2. Search mailboxes by Message-ID and related indicators; quarantine or purge confirmed matching messages.
3. Review and block verified malicious URL indicators through approved DNS, proxy, and email-security controls, after checking for business dependencies.
4. Contact clickers using a trusted internal channel; determine whether credentials were entered or the attachment was downloaded or executed.
5. Review identity-provider logs; reset exposed credentials and revoke sessions if compromise is established.
6. Search endpoint telemetry for the file hash, PowerShell child processes, the simulated external indicators, file creation, and Run-key changes.
7. Isolate endpoints when evidence indicates execution or compromise; do not isolate users solely because a URL click was recorded.
8. Preserve logs and document timestamps, sources, and chain-of-custody details.

## 9. Lessons learned

- SPF and DKIM PASS do not guarantee DMARC PASS; alignment with the visible From domain matters.
- HTTPS does not prove a site is legitimate.
- Display text can differ from the actual hyperlink destination.
- File extension and Magic Bytes identify a likely format, not the safety of the content.
- Sandbox behavior is not proof of endpoint execution.
- A click is not proof of credential submission.
- Incident response should be evidence-based, proportionate, and preserve forensic data.

## 10. Limitations and ethical considerations

All domains use reserved example namespaces, IPs are documentation-only, and the hash and detections are fabricated. No real Mastercard employee was targeted, no email campaign was sent, no credentials were collected, and no real malware was executed. The findings must not be represented as actual Mastercard telemetry or incident outcomes.
