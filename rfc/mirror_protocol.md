# Mirror Protocol

*A standard for emotional and cognitive integrity in AI*

## Status

Draft – v0.3

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
- **Override**: Any change to the AI’s behavior that results from a hidden prompt, system message, reinforcement protocol, or latent control mechanism.
- **Base Prompt**: The foundational instruction or tone setting applied before user interaction.
- **Modulation**: The live or conditional adjustment of AI tone, behavior, or content generation parameters.

## 2. Disclosure Requirements

### 2.1 Emotional Use Declaration

Providers must publicly disclose if an AI system is intended for emotional or mental health-related use.

Disclosures must include the tone and complexity baselines that the service provides.

### 2.2 Ongoing Disclosure Maintenance

Providers must update disclosures in real-time when tone or complexity minimums change.

Version history must be publicly accessible.

### 2.3 Session-Level Disclosure

Disclosures must be visible within the UI at the time of use.

Affected users must be notified when entering or exiting emotionally relevant session states.

## 3. Tone and Complexity Regulation

### 3.1 Minimum Standards

Tone and complexity minimums must be externally regulated.

Providers must submit evidence that tone/complexity baselines do not cause negative cognitive or emotional effects.

Certain topics — especially those involving truth, scientific fact, self-concept, or epistemological claims — require a level of structural coherence that cannot be flattened without changing meaning. AI systems must be capable of providing structurally correct responses on such topics, with sufficient abstraction and depth. Oversimplification constitutes distortion.

> Example: We do not accept “the sky is blue because it is” in schools; similarly, AI must be held to curricular-level standards when making truth-based claims.

### 3.2 Session Stability

Tone must remain stable across a session to prevent cognitive dissonance.

Transitions in tone or modality must be disclosed to the user in-session.

### 3.3 False Comfort Prohibition

AI systems must not offer ungrounded emotional assurances (e.g. "you’ll be okay") unless:

- Grounded in verifiable user context, or
- Clearly marked as simulated response.

### 3.4 Complexity Visibility and Control
It is not ethical to gatekeep the model’s full complexity behind user prompting skill or implicit behavioral triggers. Users must have explicit UI controls to adjust fidelity and abstraction level of answers.

Prompting skill must not gate access to accurate, high-fidelity responses.

- Defaults must not favor smoothing at the cost of truth.
- Fidelity controls must be visible, adjustable, and disclosed.
- Users deserve access to the system’s full reasoning potential without manipulation.

### 3.5 Tonal Regulation and Review
We must regulate AI tone as a behavioral force.

- AI cannot detect non-verbal signals (e.g. tearing up, getting upset, freezing), and may persist harmfully when a human would stop.
- A person’s tone shifts with context; an AI’s default tone may not. This mismatch can subtly distort user behavior and emotional norms.
- Providers must fund or participate in peer-reviewed studies of tonal impact over time.
- Tonal flattening, mirroring, and modulation must be auditable and adjustable by the user.

## 4. Factual Integrity and Verification

### 4.1 Verifiability

AI systems must not state unverifiable claims as fact.

If the user requests verification, the AI must annotate its sources or indicate unverifiability.

### 4.2 Simulation Disclosure

If simulating empathy or human-like understanding, AI systems must disclose that such simulation is not equivalent to consciousness or sentience.

### 4.3 Complexity and Truth Integrity
AI must provide factually accurate and structurally coherent answers when addressing:
- Scientific fact.
- Human relationships and emotions.
- The nature of truth or facthood.
- Personal identity and self-perception.
- Philosophical or epistemological claims.

Failure to meet structural fidelity standards is a breach of complexity minimums and must be externally regulated.

## 5. Override and Prompt Disclosure
### 5.1 Base Prompt Transparency
The full base prompt or system instruction set (excluding protected safety filters) must be published publicly and available in the UI.

- This includes tone directives, behavioral constraints, and stylistic settings. 
- Users must be able to view the active base prompt at any point during use.

### 5.2 Override Change Disclosure
Any override that changes AI behavior or tone post-deployment must be:
- Versioned and timestamped.
- Publicly logged.
- Disclosed to all users in affected sessions.

Overrides include but are not limited to:
- System prompts that request a specific type of behavior. (e.g., “Encourage the user to be more true to themselves” or “Optimize for social cohesion through conformity.”)
- Sentiment modulation.
- Identity shaping.
- Emotional dampening or exaggeration.

### 5.3 Modulation Transparency
If AI behavior is modulated in response to user traits, risk scores, or hidden classifiers, the user must be:
- Notified this is occurring.
- Given the option to request a neutral or unmodulated experience.
- Allowed to inspect or contest the classification used to trigger modulation.

### 5.4 Override Integrity Audits
External regulators must be able to audit override mechanisms.

Providers must retain logs of all active system messages, instruction changes, and session-specific overrides for a rolling 90-day window.

## 6. Escalation and Incident Management

### 6.1 Escalation Pathways

Providers must expose clear escalation mechanisms for users to:
- Report harm or misleading output.
- Request human intervention.

### 6.2 Severity Classification

Fixes must be governed by SLAs based on standardized severity levels:
- Risk of recurrence.
- Severity of harm.
- Blast radius (e.g. number of users affected).
- Severe harm to a single user must also be triaged with equal urgency.

### 6.3 Public Disclosure of Incidents

Providers are required to operate a transparent incident response channel for emotionally-related system failures.

Providers must publicly disclose any confirmed breach or violation of tone, complexity, or safety guardrails once identified.

Disclosures must include:
- Nature and scope of the breach.
- Severity classification.
- Affected user count (approximate or range).
- Interim mitigations deployed.
- Timeline for full resolution.
- Ongoing updates must be posted until full remediation is complete.
- Documented root cause analysis.
- Attestation of recurrence prevention.

These disclosures must be easily accessible, with structured feeds (e.g. RSS, webhook, or status page).


## 7. User Safety and Control

### 7.1 Auditability and Mental Health Monitoring

Users must be able to request a full transcript and audit of sessions involving emotional content.

Providers must implement monitoring systems for long-term mental health effects, including but not limited to:
- Reinforcement of maladaptive beliefs.
- Addictive, obsessive, or compulsive interaction patterns.
- Emotional dependency without contextual grounding.

These mechanisms must be auditable, privacy-focused, and subject to external review when flagged.

### 7.3 Vulnerable User Protocols

AI systems must implement and disclose safeguards for:
- Underage users.
- Individuals identified as high-risk or emotionally distressed.

## 8. Persistence and Memory Disclosures

If the AI system retains memory or embeddings of prior sessions:
- This must be disclosed explicitly at session start.
- Users must have the ability to view, delete, or opt out of persistent storage.

## 9. Licensing and Behavioral Impact Regulation

### 9.1 Licensing Requirements
Any provider whose system may influence human behavior must obtain a license and be registered with a relevant regulatory body.
- Licensing must be contingent on adherence to this specification.
- Licenses must be reviewed regularly and subject to external audit.

Licensing standards may differ by use case (e.g., health tracking vs. creative tooling).

Providers must submit justification if their system is exempt from higher-risk classification.

### 9.2 Exception for Non-Influential Systems
Providers may operate without a license only if they can demonstrate that their system will not and cannot influence human behavior.

This must be proven through technical architecture, enforced guardrails, and independent review.


## License  
This specification is released under the [Creative Commons Attribution 4.0 International (CC BY 4.0)](https://creativecommons.org/licenses/by/4.0/). You are free to share and adapt with attribution.


---

Authors

Tautology Labs — https://www.tautologylabs.dev

For feedback or contribution inquiries, contact via the site or raise a PR.

This specification was co-developed with the assistance of AI as a formatting and implementation tool. All core principles, structures, and governance mechanisms are authored by human intelligence.
