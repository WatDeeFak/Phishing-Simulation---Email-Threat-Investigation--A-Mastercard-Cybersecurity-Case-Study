# Lessons Learned

## Technical lessons

- SPF checks whether the sending source is authorized by the evaluated SPF domain; it does not validate the message's safety.
- DKIM verifies a cryptographic signature and the integrity of signed content; it does not prove the sender's intent is benign.
- DMARC requires SPF or DKIM to pass and align with the visible From domain.
- The visible hyperlink label may differ from the actual `href` destination.
- A redirect parameter needs safe behavior validation before claiming an open-redirect vulnerability.
- HTTPS protects transport; it does not make a phishing site legitimate.
- File extensions can be misleading; magic bytes help identify the likely file format.
- SHA-256 identifies file content; the hash itself is not a malware verdict.
- Sandbox observations must not be confused with execution on an employee endpoint.

## Investigation lessons

- Correlate related artefacts without assuming common ownership or actor identity.
- Distinguish evidence, inference, and unknowns in every report.
- A URL click does not mean a password was entered.
- A delivered attachment does not mean it was executed.
- An observed sandbox behavior does not prove a real endpoint was compromised.
- Preserve original artefacts and relevant logs before remediation where feasible.

## Professional development

The main skill developed in this case study is evidence-based reasoning: make claims that the data supports, document limitations, and select proportionate response actions. A good investigation is not the one with the most severe conclusion; it is the one with the most defensible conclusion.
