# Checkov: strengths and tradeoffs

| Strength | Why it is useful in this implementation |
| --- | --- |
| **Early infrastructure feedback** | Inspect Terraform definitions before deployment to catch insecure configuration choices while they are still reviewable source changes. |
| **Broad built-in control library** | Rule IDs and resource-level evidence organize checks across storage, networking, logging, identity and availability; custom policies can complement built-in controls. |
| **Actionable triage** | Repeatable resource/file identities, counts and next-evidence tracking support focused remediation without confusing a static finding with live compromise. |

| Limit | Practical response |
| --- | --- |
| Static context is incomplete | External/omitted modules, variable resolution and modern alternative controls can require further evidence. |
| Finding is not exploitability | A failed rule may represent cost/availability policy or a missing static graph relationship, not proven compromise. |
| Advisory is not approval | This actual wrapper uses soft-fail for findings; execution, version, parse and coverage errors still fail. It is not a release security gate. |

## Choosing the right layer

Trivy inventories/scans supported packages and images, with separate configuration capability. TruffleHog focuses on possible credentials and Git-history coverage. Checkov focuses on infrastructure definitions and policy rules. ZAP, used separately by the platform, exercises HTTP behavior; it is not replaced by any of these source scans.

Keep all three outputs tied to an explicit target and date. Tool severity, an organization's release threshold, exploitability and a business risk-acceptance decision are different concepts. A passing narrow check does not certify the entire environment.

The upstream tool documentation describes broader capabilities than every mode used here. The implemented mode and its privacy/network restrictions are established by mapped source and dated tests. [Official Checkov reference](https://www.checkov.io/2.Basics/CLI%20Command%20Reference.html).
