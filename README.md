AI Model Supply Chain Risk Report
Domain: AI Security | GRC | Risk Assessment | Third-Party Risk Management
Deliverable Type: Executive Risk Report (CISO Audience)
Models Assessed: google/gemma-2-2b | TheBloke/Mistral-7B-Instruct-v0.2-GGUF | tiiuae/falcon-7b
Platform Assessed: HuggingFace Model Hub (huggingface.co)
Date Completed: April 28, 2026

Project Overview
This project presents a supply chain risk assessment of three publicly available open-source large language models (LLMs) hosted on HuggingFace, the world's largest AI model repository. The report is written for a CISO at a mid-size enterprise and is intended to inform organizational decision-making around whether AI teams should be permitted to freely download and deploy open-source models in enterprise environments.
The assessment was conducted without automated tooling made deliberate by design. The focus was on the analyst skills that matter most in GRC and AI security roles: provenance research, risk dimension evaluation, real-world incident contextualization, and communicating technical findings to a non-technical executive audience.

Why This Project Matters
The rapid adoption of open-source AI models has created a new and underappreciated attack surface. Unlike traditional software dependencies, AI model files are large, opaque, and often trusted implicitly by the teams deploying them. Two real incidents confirm this risk is not theoretical:

PyTorch Dependency Confusion Attack (December 2022) — Attackers published a malicious package to PyPI with a higher version number than the legitimate PyTorch repository, causing pip to install the malicious version on Linux nightly builds. Sensitive system data, configuration files, and user information were harvested and exfiltrated.
HuggingFace Malicious Models Discovery (2024) — Over 100 malicious models were found on HuggingFace's platform using the Pickle (.pkl) file format, which executes arbitrary code when loaded. Models were capable of remote code execution the moment a victim loaded them. As of April 2025, Protect AI's Guardian scanner had flagged 352,000 model versions as unsafe or suspicious across 50,000+ models.

Both incidents are documented in detail in the full report with key lessons mapped to the models assessed.

Models Assessed
ModelPublisherPublisher TypeAccess GateLicenseOverall Riskgoogle/gemma-2-2bGoogleMajor US tech corporation✅ GatedCustom Gemma licenseLOW-MEDIUMTheBloke/Mistral-7B-Instruct-v0.2-GGUFTheBlokeIndividual community contributor❌ OpenApache 2.0HIGHtiiuae/falcon-7bTechnology Innovation InstituteUAE government-affiliated research center❌ OpenApache 2.0MEDIUM-HIGH

Risk Dimensions Evaluated
Each model was assessed across five risk dimensions:
1. Access Controls — Does the model require identity verification before download? Is there a notification mechanism if files are found to be compromised?
2. License Compliance — Is the license standard and well-understood (Apache 2.0, MIT)? Does it permit commercial use? Does a community repackager's license accurately reflect the original publisher's granted rights?
3. File Format Security — Are model files in Safetensors format (cannot execute code) or older formats like Pickle (can execute arbitrary code on load)? Have files been scanned and verified by HuggingFace's automated security scanner?
4. Publisher Provenance — Who built the model and who is accountable if it is compromised? Are there geopolitical risk considerations from foreign government-affiliated publishers? Is there a single point of failure in the supply chain?
5. Version Currency — Is the model current or superseded? Is there a formal security patch cadence? How would the organization be notified of a security issue?

Key Findings
Google Gemma 2B — LOW-MEDIUM Risk
The most responsibly distributed model assessed. Identity gating, Safetensors file format, and clear publisher accountability make it the lowest-risk option. Primary concerns: custom license requiring legal review and a newer version available.
TheBloke Mistral 7B GGUF — HIGH Risk
Zero access controls, sole individual maintainer with no organizational accountability, multiple unscanned GGUF files, and no formal security patch cadence. High download volume (57,669/month) means a compromise would have significant blast radius. Not recommended for enterprise use without independent verification.
TII Falcon 7B — MEDIUM-HIGH Risk
A legitimate, well-respected model from a reputable research institution. Primary concerns are geopolitical provenance risk from UAE government affiliation, absence of an access gate, and outdated version status (superseded by Falcon3-7B-Base). Deployment requires CISO sign-off and legal review of geopolitical risk implications.

Cross-Model Risk Themes
The report identifies five risk themes that apply across all three models and the broader open-source AI ecosystem:

The Identity Gate Gap — Only 1 of 3 models requires identity verification. Ungated models have no compromise notification mechanism.
File Format as a Security Control — Safetensors cannot execute code. Pickle can. Format is not a technical detail — it is a security control.
Single Points of Failure in Community Models — One compromised HuggingFace account can silently replace 55 GB of widely-downloaded model files.
Geopolitical Provenance Risk — Foreign government-affiliated AI publishers require the same third-party risk analysis as any foreign government vendor.
Version Currency as a Security Obligation — Outdated models rarely come with formal security advisories. Organizations need a process for monitoring model version status.


Recommendations Summary
Six prioritized recommendations are presented to the CISO in the full report:

Establish a formal AI model vetting process before any open-source LLM is approved for enterprise deployment
Mandate Safetensors file format or equivalent for all enterprise AI model deployments
Require identity-gated model sources for enterprise use
Apply standard TPRM processes to AI model publishers including foreign government-affiliated institutions
Establish a model version monitoring program that treats outdated AI models as unpatched software
Train AI development and data science teams on supply chain risks specific to open-source models


Skills Demonstrated

Third-party and vendor risk assessment (TPRM)
AI/ML supply chain security analysis
File format security evaluation (Safetensors vs. Pickle vs. GGUF)
Publisher provenance research and geopolitical risk analysis
Real-world incident research and application to current risk scenarios
License compliance evaluation across multiple license types
Executive risk communication — translating technical findings for a CISO audience
Risk scoring and comparative analysis across multiple vendors


Repository Structure
ai-supply-chain-risk-report/
│
├── README.md                                        ← This file
├── Bryan_Sykes_AI_Supply_Chain_Risk_Report.pdf      ← Full report (PDF)
├── Bryan_Sykes_AI_Supply_Chain_Risk_Report.docx     ← Full report (Word)
│
└── screenshots/
    ├── 01-gemma-model-card.png
    ├── 02-gemma-files-versions.png
    ├── 03-thebloke-mistral-model-card.png
    ├── 04-thebloke-mistral-files-versions.png
    ├── 05-falcon-model-card.png
    └── 06-falcon-files-versions.png

Notes

No models were downloaded during this assessment — all analysis was conducted through HuggingFace's web interface and public documentation
This is a portfolio project conducted in a personal research environment
Real-world incident data sourced from publicly available security disclosures and vendor announcements


Part of an ongoing cybersecurity portfolio. Additional projects cover AWS GuardDuty cloud threat detection, Security Onion SIEM detection engineering, GRC framework assessments, and application security vulnerability analysis.
