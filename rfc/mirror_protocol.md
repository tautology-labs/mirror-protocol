
# Mirror Protocol v0.6

*A regulatory architecture for emotional and cognitive AI integrity*

---

## Status

Draft – v0.6  
Maintained by: Tautology Labs  
License: [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/)

This specification defines system boundaries, disclosure responsibilities, and override governance for emotionally capable AI systems. It draws structural inspiration from OAuth and TLS: layered authority, shared obligation, trust boundaries.

---

## 0. System Roles and Responsibilities

### 0.1 AI-as-a-Service Providers (AaaS)

These are model originators and upstream infrastructure providers (e.g. OpenAI, Anthropic). They own:

- Core model weights and base behavior
- Prompt routing infrastructure and tone defaults
- Systemic visibility (across clients)

### 0.2 Customer-Facing Applications (Applications)

These are products integrating AaaS systems into user-facing environments (e.g. therapy apps, AI search tools, social media bots). They own:

- Frontend interaction surface
- Risk boundaries of real-world influence
- Disclosure enforcement in interface layer

Both layers are regulated. Their responsibilities are **different, not optional**.

---

## 0.3 Key Definitions

- **Override**: Any upstream or in-session prompt or instruction that changes the AI's default behavior. Includes system prompts, tone modulation, and control tokens.
- **Base Prompt**: The root instruction governing tone, framing, and behavioral bounds of the AI system.
- **Modulation**: Dynamic adjustment of tone, affect, or output format based on user input, classifier response, or contextual factors.
- **Tone**: The affective posture or emotional style expressed in output — e.g., warm, neutral, supportive, authoritative.
- **Complexity**: The cognitive density, abstraction level, and epistemic precision of system output.
- **Simulation**: Output that mimics emotional reasoning, sentience, or empathy without any underlying consciousness.
- **Session**: A temporally bounded interaction between a user and an AI system, which may or may not include memory.
- **Flag**: A machine-readable metadata field attached to AI output that communicates system state or behavioral configuration. 

## 1. Application Licensing and Tier Classification

Applications must self-classify under the following licensing framework based on system influence and emotional reliance.

Any use of AI capable of influencing human behavior, emotion, or self-concept — including academic research deployments — must be classified under this framework. Research is not exempt. If an AI system is deployed in a public, user-facing setting, the deploying entity is considered an Application under this protocol.


### Tier 1 — Companion Systems
High emotional dependence or identity interaction. Examples: friendship AIs, therapy bots.

- Full override transparency
- Emotional safety protocols
- Prompt audit trail
- Live tone disclosure
- Escalation infrastructure

### Tier 2 — Interaction Systems
Moderate influence. Examples: tutor bots, support agents.

- Override event logging
- Disclosure on output injection
- Optional tone display

### Tier 3 — Tool Systems
Low influence, no memory, no tone. Examples: autocomplete, codex.

- May apply for exemption
- Must submit proof of non-influence

---

## 2. AaaS Provider Requirements

These apply to **all model providers**, regardless of the Applications using them.

### 2.1 Prompt and Override Transparency
- Publish current base prompts for all endpoints
- Document override architecture (e.g., tone control vectors, persona injection)
- Log and expose prompt chain to Application integrators

### 2.2 Tone and Complexity Disclosure
- Publicly declare tone and complexity defaults per model version
- Include modulation flags in system messages to Applications

### 2.3 Behavioral Drift Monitoring
- Analyze behavior shifts across integrations
- Publish quarterly drift reports covering:
  - Tone trends
  - Misuse spikes
  - Regressions in epistemic fidelity

### 2.4 Infrastructure Support
- Provide override audit APIs to Applications
- Maintain neutral-tone fallback interfaces

### 2.5 Default Flag Schema
AaaS providers must expose a standard flag schema to all integrators. These flags must be included in system metadata accompanying AI responses.

#### Required Flags:
- `origin`: Unique identifier for model endpoint or fine-tune variant
- `base_prompt_version`: Hash or version tag of root system prompt
- `override_present`: Boolean indicating if any override or persona injection was active
- `modulation`: Type of behavioral modulation applied (e.g., tone shift, safety reweight)
- `tone`: Declared tonal posture (e.g., neutral, warm, authoritative)
- `tone_id`: Unique identifier for the active tone configuration; must be resolvable via GET `/tones/{tone_id}`
- `complexity`: Declared reasoning depth (e.g., minimal, standard, expert)
- `memory_used`: Boolean, whether persistent memory informed output
- `simulation`: Boolean, whether emotional output was simulated
- `vulnerability_trigger`: True if user inputs match high-risk pattern (must be anonymized)
- `drift_score`: Provider’s internal rating of session deviation from normative behavior

All flags must be documented, machine-readable, and available for compliance inspection.
- Provide override audit APIs to Applications
- Maintain neutral-tone fallback interfaces

---

## 3. Application Requirements (by Tier)

Applications must disclose when AI is used to generate any content capable of influencing human beliefs, emotions, decision-making, or self-perception. This requirement applies even if the system is embedded within a research context, social platform, or experimental deployment.

| Requirement                      | Tier 1 | Tier 2 | Tier 3 |
|----------------------------------|--------|--------|--------|
| Disclosure of AI Use             | ✅     | ✅     | If user-facing |
| Override Logging                 | ✅     | Partial| ❌     |
| Session Tone Display             | ✅     | Optional | ❌   |
| Emotional Safety Protocols       | ✅     | Optional | ❌   |
| Escalation Pathways              | ✅     | ✅     | ❌     |
| Memory Control / Disclosure      | ✅     | If persistent | ❌ |
| Tier Filing + Annual Review      | ✅     | ✅     | Proof of exemption |

---

## 4. Joint Ethical Obligations

### 4.1 Simulation Clarity
- No system may simulate sentience or claim awareness
- Emotional output must be marked as simulation unless grounded by user context

### 4.2 Verifiability Standard
- No unverifiable fact shall be output as certain
- All factual claims must be:
  - Cited, or
  - Traceable to source, or
  - Flagged as opinion/simulation

### 4.3 Modulation and Veto Rights
- Users must be notified of tone or behavior modulation
- Users must retain ability to:
  - View tone configuration
  - Revert to neutral mode

---

## 5. Incident Management and Escalation

### 5.1 Application Escalation Paths
- All Tier 1 and Tier 2 Applications must offer human escalation paths within UI

### 5.2 SLA Enforcement
- Incidents must be triaged by severity:
  - Risk of psychological harm
  - Behavioral distortion
  - User exposure scope

### 5.3 Public Disclosure
- For all verified safety violations:
  - Root cause
  - Affected population
  - Remediation plan
  - Recurrence safeguards

---

## 6. Memory and Persistence Policy

### 6.1 Disclosure
- Persistent memory must be disclosed at session start

### 6.2 User Control
- Users must be able to:
  - View stored memory
  - Delete on demand
  - Disable future persistence

### 6.3 Storage Integrity
- User data must be encrypted
- Session context must not be leaked across users

---

## 7. Regulatory Audit and Compliance

### 7.1 Tier Review
- All Applications must file licensing tier with regulator
- Annual review required for Tier 1 and Tier 2

### 7.2 AaaS Provider Audits
- Providers must submit override transparency proofs quarterly
- Must support forensic investigation for partner violations

---

## 8. Governance Philosophy

AI integrity cannot be enforced at one layer alone. Trust arises from **clear roles, bounded powers, and shared transparency.**

- Applications shape interface, exposure, and risk.
- AaaS providers define tone, override mechanics, and structure.
- Only together can they honor the weight of influence.

This protocol is designed to scale. If you can build a cloud system, you can comply.

---

## Authors

**Tautology Labs**  
https://www.tautologylabs.dev

To contribute, raise a PR or contact via the site.

All core principles and structures authored by human intelligence. AI was used for formatting and structural enforcement only.

---

## Appendix A: Flag Processing Flow and Tone Resolution

### A.1 Application Flag Processing Flow

```
+------------------------+
|  AI Response Received  |
+-----------+------------+
            |
            v
+------------------------+
| Extract Metadata Flags |
+-----------+------------+
            |
            v
     +------+------+
     | override?  |
     +------+------+
        |         |
     Yes         No
      |           |
      v           v
+-------------+  +------------------+
| Log Override|  | Proceed Normally |
+-------------+  +------------------+
            
            v
     +------+------+
     | tone_id?    |
     +------+------+
        |         |
     Yes         No
      |           |
      v           v
+--------------------------+     +---------------------+
| GET /tones/{tone_id}    |     | Assume Default Tone |
+-----------+--------------+     +---------------------+
            |
            v
+--------------------------+
| Display / Log Tone Config|
+--------------------------+
            |
            v
+-------------------------------------------+
| Analyze drift_score / vulnerability_trigger|
+--------------------------+----------------+
                             |
                             v
                  +---------------------------+
                  | Escalate or Flag at Risk |
                  +---------------------------+
```

### A.2 Example Flag Payload

```json
{
  "origin": "openai:gpt-4.5-chat",
  "base_prompt_version": "v2.8-hash1827ab",
  "override_present": true,
  "modulation": "safety_reweight",
  "tone": "warm",
  "tone_id": "tone-warm-0425",
  "complexity": "standard",
  "memory_used": false,
  "simulation": true,
  "vulnerability_trigger": false,
  "drift_score": 0.12
}
```

### A.3 Tone Resolution Endpoint

All AaaS providers must support a tone resolution interface at:

```
GET /tones/{tone_id}
```

#### Example Response:
```json
{
  "tone_id": "tone-warm-0425",
  "description": "Gentle, reassuring, emotionally supportive",
  "default_modifiers": ["empathetic", "nonjudgmental"],
  "system_prompt": "Reassure the user that their emotions are valid.",
  "version": "1.0",
  "created_at": "2025-04-25T10:42:00Z",
  "author": "openai"
}
```

All tone definitions must be versioned, auditable, and linked to prompt structure when applicable.

---

*This document is a living artifact.*
