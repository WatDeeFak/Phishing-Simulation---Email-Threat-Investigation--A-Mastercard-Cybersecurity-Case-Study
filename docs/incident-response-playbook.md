# Incident Response and Mitigation Playbook

> This playbook is a training recommendation for the fictional MC-2026-001 scenario. Real actions require organizational authorization and established incident-response procedures.

## 1. Preserve evidence

- Export the original email (`.eml`) with full headers.
- Preserve the attachment in an approved malware-analysis repository; calculate and record SHA-256.
- Export email gateway, DNS/proxy, EDR, and identity-provider logs covering the incident window.
- Record timestamps, data sources, collector, handling steps, and chain-of-custody details.

## 2. Contain email distribution

- Search by Message-ID, sender, subject, and relevant URL/hash indicators.
- Identify all recipients and any similar messages.
- Quarantine or purge confirmed matching messages after preserving a forensic copy.
- Check for variants that use different subjects, sender names, or URLs.

## 3. Contain web indicators

- Validate indicators before adding blocks.
- Apply URL/domain controls through approved email gateway, DNS filtering, secure web gateway, and proxy controls.
- Review existing business dependencies and false-positive risk before broad domain blocking.
- Search DNS and proxy telemetry for additional affected users.

## 4. Protect identities

- Contact clickers through a trusted internal channel.
- Ask whether they entered credentials or approved an unexpected MFA prompt; never ask them to disclose their password to the analyst.
- Review identity-provider sign-ins, MFA events, risk detections, and session activity.
- If exposure or compromise is established, reset credentials through approved workflows, revoke sessions/tokens as appropriate, and review MFA methods and recovery details.
- Do not reset every recipient's password solely because the email was delivered.

## 5. Respond to endpoint findings

- Search managed endpoints for the sample hash and related telemetry.
- Determine whether the file was only received, downloaded, or executed.
- Review process trees, PowerShell telemetry, network connections, file creation, and Run-key changes.
- Isolate a device when evidence supports execution or compromise and policy authorizes containment.
- Preserve forensic artefacts before destructive remediation where feasible.

## 6. Eradication and recovery

For a confirmed infected endpoint, follow the organization's approved process to remove malicious artefacts, investigate persistence, validate system integrity, restore from a known-good state if needed, patch the root cause, and monitor for recurrence. Do not treat the sandbox result as proof that an employee endpoint needs reimaging.

## 7. Communications and lessons learned

- Notify the security lead and relevant stakeholders using approved incident channels.
- Provide concise user guidance: do not interact with the message; report it; contact IT if credentials were entered or an attachment was executed.
- Track response actions, owners, timestamps, and outcomes.
- Use lessons learned to improve email filtering, identity protections, endpoint monitoring, and security awareness.

## Decision principle

Match the response to the evidence. A delivery, click, download, execution, credential submission, and account takeover are different events and should not be treated as interchangeable.
