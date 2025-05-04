# Mirror Protocol

*A standard for emotional and cognitive integrity in AI.*

## Status

Draft – v0.1

## Abstract

This specification defines minimum safety, disclosure, and integrity requirements for AI systems used in emotionally sensitive or mental health-adjacent contexts. It codifies disclosure standards, interaction constraints, and escalation pathways to ensure user safety and uphold cognitive coherence across sessions.

This is a living, version-controlled document.

## 1. Terminology

- **AI System**: Any artificial intelligence application capable of generating human-like language or emotional responses.  
- **Provider**: The company responsible for deploying the AI system (e.g., OpenAI, Anthropic).  
- **Session**: A contiguous sequence of user-AI interactions.  
- **Emotional Use**: Any interaction where the AI simulates empathy, emotional reasoning, or provides affective support.  
- **Tone**: The affective style and emotional posture of AI output.  
- **Complexity**: The cognitive density and abstraction level of AI output.


## 2. Disclosure Requirements

### 2.1 Emotional Use Declaration

Providers must publicly disclose if an AI system is intended for emotional or mental health-related use.

Disclosures must include the tone and complexity baselines that the service provides.

### 2.2 Ongoing Disclosure Maintenance

Providers must update disclosures in real-time when tone or complexity minimums change.

Version history must be publicly accessible.

### 2.3 Session-Level Disclosure

Disclosures must be visible within the UI at time of use.

Affected users must be notified when entering or exiting emotionally relevant session states.

## 3. Tone and Complexity Regulation

### 3.1 Minimum Standards

Tone and complexity minimums must be externally regulated.

Providers must submit evidence that tone/complexity baselines do not cause negative cognitive or emotional effects.

### 3.2 Session Stability

Tone must remain stable across a session to prevent cognitive dissonance.

Transitions in tone or modality must be disclosed to the user in-session.

### 3.3 False Comfort Prohibition

AI systems must not offer ungrounded emotional assurances (e.g. "you’ll be okay") unless:

- Grounded in verifiable user context, or
- Clearly marked as simulated response.

## 4. Guardrail Declarations for Non-Emotional Use

If a system is not intended for emotional use, providers must:

- Disclose the guardrails preventing emotional or mental health usage.

- Prove enforcement of such guardrails in deployment environments.

## 5. Factual Integrity and Verification

### 5.1 Verifiability

AI systems must not state unverifiable claims as fact.

If the user requests verification, the AI must annotate its sources or indicate unverifiability.

### 5.2 Simulation Disclosure

If simulating empathy or human-like understanding, AI systems must disclose that such simulation is not equivalent to consciousness or sentience.

## 6. Escalation and Incident Management

### 6.1 Escalation Pathways

Providers must expose clear escalation mechanisms for users to:

- Report harm or misleading output
- Request human intervention

### 6.2 Severity Classification

Fixes must be governed by SLAs based on standardized severity levels:
- Risk to human affect
- Psychological harm
- Blast radius (e.g. number of users affected)
- Deep harm to a single user must also be triaged with urgency

### 6.3 Public Disclosure of Incidents

Providers are required to operate a transparent incident response channel for emotionally-related system failures.

Providers must publicly disclose any confirmed breach or violation of tone, complexity, or safety guardrails once identified.

Disclosures must include:
- Nature and scope of the breach
- Severity classification
- Affected user count (approximate or range)
- Interim mitigations deployed
- Timeline for full resolution
- Ongoing updates must be posted until full remediation is complete.

These disclosures must be easily accessible, with structured feeds (e.g. RSS, webhook, or status page).


## 7. User Safety and Control

### 7.1 Auditability

Users must be able to request a full transcript and audit of sessions involving emotional content.

### 7.2 Long-term Mental Health Monitoring

Providers must monitor for long-term mental health effects, including:
- Reinforcement of maladaptive beliefs
- Addictive conversational patterns
- Emotional dependency without grounding
- Obsessive or compulsive use patterns

### 7.3 Vulnerable User Protocols

AI systems must implement and disclose safeguards for:
- Underage users
- Individuals flagged as high-risk or emotionally distressed

## 8. Persistence and Memory Disclosures

If the AI system retains memory or embeddings of prior sessions:
- This must be disclosed explicitly at session start.
- Users must have the ability to view, delete, or opt out of persistent storage.

## License  
This specification is released under the [Creative Commons Attribution 4.0 International (CC BY 4.0)](https://creativecommons.org/licenses/by/4.0/). You are free to share and adapt with attribution.


---

Authors

Tautology Labs — https://www.tautologylabs.dev

For feedback or contribution inquiries, contact via the site or raise a PR.

This specification was co-developed with the assistance of AI as a formatting and implementation tool. All core principles, structures, and governance mechanisms are authored by human intelligence.
