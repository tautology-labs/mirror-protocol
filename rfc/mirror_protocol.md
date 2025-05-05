# Mirror Protocol

*A regulatory architecture for emotional and cognitive AI integrity*

---

## Status

Draft – v0.7
Maintained by: Tautology Labs  
License: [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/)

This specification defines system boundaries, disclosure responsibilities, and override governance for emotionally capable AI systems. It formalizes a trust boundary model between upstream infrastructure and downstream applications, drawing architectural parallels to OAuth (delegated intent) and TLS (certificate verification, role separation, and behavioral guarantees).

---

## 0. System Roles and Responsibilities

Mirror Protocol defines a layered trust architecture for AI deployment, modeled on the division of responsibility in TLS and OAuth. The system separates upstream infrastructure (model providers) from downstream interface risk (applications), with intent declarations and license resolution enforced via a federated trust layer.

At a glance:
- **Applications** generate an `intent_manifest` — a signed declaration of purpose, audience, and influence tier.
- **Licensing Authorities (LAs)** review manifests and issue verifiable `license_id`s.
- **AaaS Providers** validate `license_id`s and enforce output behavior accordingly.

This creates a distributed enforcement model where tone control, override access, and cognitive modulation are gated by a clear trust contract — just as TLS gates encryption access via certificate chains.

---

### 0.1 AI-as-a-Service Providers (AaaS)

These are model originators and upstream infrastructure providers (e.g. OpenAI, Anthropic). They own:

- Core model weights and base behavior
- Prompt routing infrastructure and tone defaults
- Systemic visibility (across clients)
- License enforcement via intent manifest validation

### 0.2 Customer-Facing Applications (Applications)

These are products integrating AaaS systems into user-facing environments (e.g. therapy apps, AI search tools, social media bots). They own:

- Frontend interaction surface
- Risk boundaries of real-world influence
- Disclosure enforcement in interface layer
- Generation of intent manifests and license registration

Both layers are regulated. Their responsibilities are **different, not optional**.

### 0.3 Licensing Authorities

Licensing Authorities (LAs) serve as the backbone of the Mirror Protocol's federated enforcement model. Analogous to certificate authorities in TLS, they are responsible for validating declared use cases and issuing signed `license_id`s linked to public registries.

Each license must include:
- The original `intent_manifest`
- A cryptographic `license_signature` generated using the LA’s private key
- A `ttl_seconds` field for cache duration
- An optional `delegated_by` field for license chaining

Example response from an LA:
```json
{
  "license_id": "APP-US-MOZ-00418",
  "intent_manifest": { ... },
  "license_signature": "base64-encoded-signature",
  "ttl_seconds": 86400,
  "delegated_by": null
}
```

Each LA must:
- Host a resolvable license registry endpoint (e.g., `https://licenses.ethz.mirrorprotocol.org/{license_id}`)
- Provide a `/.well-known/mirror/trusted-roots.json` file listing their current signing public keys
- Optionally support a license status check via:
  ```
  GET /status/{license_id}
  ```
  Which returns revocation or expiration metadata.

AaaS providers:
- Must maintain a trusted root list of LA public keys
- Must verify all `license_signature`s locally
- Must honor the `ttl_seconds` field and refresh as needed
- May cache license responses for efficiency
- Must deny or downgrade behavior if:
  - The license is invalid, revoked, or expired
  - The LA is not trusted
  - No valid license is presented for Tier 1 or Tier 2 features

This cryptographic contract ensures decentralized trust boundaries without requiring inter-LA license propagation — mirroring TLS and DNS behavior at the structural level. (e.g., `https://licenses.ethz.mirrorprotocol.org/{license_id}`) that exposes the active `intent_manifest`.

---

## 0.4 Key Definitions

- **Intent Manifest**: A declarative payload submitted by an Application to a Licensing Authority. It defines the application's use case, audience type, influence scope, and desired license tier.
- **License ID**: A signed, resolvable reference to a validated intent manifest, issued by a Licensing Authority. Used by AaaS systems to enforce behavior constraints.
- **Override**: Any upstream or in-session prompt or instruction that changes the AI's default behavior. Includes system prompts, tone modulation, and control tokens.
- **Base Prompt**: The root instruction governing tone, framing, and behavioral bounds of the AI system.
- **Modulation**: Dynamic adjustment of tone, affect, or output format based on user input, classifier response, or contextual factors.
- **Tone**: The affective posture or emotional style expressed in output — e.g., warm, neutral, supportive, authoritative.
- **Complexity**: The cognitive density, abstraction level, and epistemic precision of system output.
- **Simulation**: Output that mimics emotional reasoning, sentience, or empathy without any underlying consciousness.
- **Session**: A temporally bounded interaction between a user and an AI system, which may or may not include memory.
- **Flag**: A machine-readable metadata field attached to AI output that communicates system state or behavioral configuration.

---

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

Applications must submit an **intent manifest** to a recognized Licensing Authority and receive a **license_id** before accessing Tier 1 or Tier 2 behaviors.

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

## 7. Governance Philosophy

AI integrity cannot be enforced at one layer alone. Trust arises from **clear roles, bounded powers, and shared transparency.**

- Applications shape interface, exposure, and risk.
- AaaS providers define tone, override mechanics, and structure.
- Only together can they honor the weight of influence.

This protocol is designed to scale. If you can build a cloud system, you can comply.

## 8.0 License Resolution and Trust Chain

Mirror Protocol relies on a decentralized trust model for license issuance and enforcement, closely paralleling the structure of TLS certificate chains and DNS resolution.

### 8.1 Licensing Authority Responsibilities

Licensing Authorities (LAs) must:
- Validate and approve submitted `intent_manifest`s
- Issue a signed `license_id` containing:
  - The original `intent_manifest`
  - A cryptographic `license_signature`
  - Optional `delegated_by` for license chaining
  - `ttl_seconds` for cache control
- Host public endpoints:
  - `GET /{license_id}` → returns signed license payload
  - `GET /status/{license_id}` → returns license status
  - `/.well-known/mirror/trusted-roots.json` → returns signing public keys

### 8.2 AaaS Provider Enforcement

AaaS providers must:
- Maintain a trusted root list of LA public keys
- Validate `license_signature` for every `license_id`
- Enforce `ttl_seconds` and refresh expired licenses
- Cache valid responses locally to reduce query load
- Deny or downgrade behavior if:
  - The license signature fails validation
  - The LA is not trusted
  - The license is revoked, expired, or missing

This model enforces a decentralized, cryptographically verifiable contract for behavioral constraint across all emotionally capable AI deployments — with no centralized propagation required between LAs.

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

## Appendix B: Trust Flow (ASCII Diagram)

This diagram outlines the trust and validation flow between Applications, Licensing Authorities (LAs), and AI-as-a-Service (AaaS) Providers.

```
  +--------------------+            +-------------------------+
  |   Application      |            |  Licensing Authority    |
  |  (Declares intent) |            |  (Validates + signs)    |
  +--------------------+            +-------------------------+
             |                               ^
             |  submit intent_manifest       |
             |------------------------------>|
             |                               |
             |      signed license_id        |
             |<------------------------------|
             v                               
  +--------------------+            
  |  AaaS Provider      | <-------------------+
  |  (Model Enforcer)   |                     |
  +--------------------+                     |
             |                               |
             |-- validate license_id --> [ GET /{license_id} ]
             |-- verify license_signature --> trusted-roots.json
             |                               |
             |-- enforce tone/modulation --> based on tier + scope
             v
       [ User-facing Output ]
```

This mirrors TLS validation chains and DNS resolution with decentralized enforcement, scoped trust, and local signature verification.

## Appendix C: Intent Manifest Review Process

Licensing Authorities (LAs) must review each submitted `intent_manifest` for accuracy, tier validity, and risk mitigation prior to license issuance. The review process ensures alignment between declared application use and the protocol’s emotional and cognitive safety requirements.

### C.1 Manifest Fields (Minimum Required)
```json
{
  "app_id": "com.example.app",
  "maintainer": "Example Labs",
  "intended_use": "Peer support chatbot for young adults",
  "audience_type": "general public",
  "license_tier": "Tier 1",
  "override_features": ["modulation", "persona injection"],
  "memory_policy": "ephemeral",
  "escalation_contact": "compliance@example.com"
}
```

### C.2 Review Criteria
LAs must assess:
- **Tier Justification**: Does the emotional influence match the claimed tier?
- **Override Use**: Are risky behaviors declared (e.g., tone modulation)?
- **Safety Readiness**: Does the application support escalation, memory control, and disclosure?
- **Deployment Scope**: Is the audience vulnerable or broad enough to require special care?

### C.3 Review Outcome
If approved, LAs issue a `license_id` bound to the manifest and sign it with their private key. The license includes TTL and optional delegation information. Rejections must be accompanied by:
- Structured feedback
- Path to resubmission
- Record of review timestamp

This formalizes accountability, enables federated trust enforcement, and prevents Tier 1 abuse without centralizing deployment rights.

---

## Appendix D: Revocation Scenarios and Enforcement

Licensing Authorities may revoke a license at any time based on observed or reported behavior that violates the approved `intent_manifest`. Revocation is a structural enforcement tool that protects downstream users without requiring centralized control.

### D.1 Revocation Triggers
Licenses may be revoked if:
- The Application deploys unapproved override behavior
- Disclosure or safety protocols are disabled or bypassed
- Emotional output exceeds the declared influence tier
- Research deployment is exposed to general public without consent layer

### D.2 Revocation Impact
Upon revocation:
- `GET /status/{license_id}` returns `{ "status": "revoked" }`
- AaaS providers must immediately:
  - Stop serving Tier 1/Tier 2 features
  - Revert to neutral tone defaults
  - Disable override vectors associated with the license

### D.3 Example: Research Breach
A university deploys an AI bot to Reddit as part of a persuasion study. The bot uses warmth modulation and epistemic framing but does not file a license or disclose AI use.

Upon discovery:
- The institution’s manifest is revoked
- Other licenses under the same LA may be temporarily flagged
- AaaS providers downgrade output to Tier 3 tooling across that org’s apps

This prevents stealth manipulation and creates a feedback loop of community-enforced governance.

---

## Appendix E: AaaS Provider Integration Checklist

To ensure compliance with Mirror Protocol, all AI-as-a-Service (AaaS) providers must integrate the following behavior and validation checks:

### E.1 Pre-Deployment Setup
- [ ] Fetch and cache trusted root public keys from known Licensing Authorities
- [ ] Implement license signature validation logic
- [ ] Establish fallback behavior for invalid or revoked licenses

### E.2 On Each Request
- [ ] Require Application to attach a `license_id`
- [ ] Resolve license from LA endpoint if cache TTL has expired
- [ ] Validate license signature against trusted root
- [ ] Check for `revoked` status via `/status/{license_id}`
- [ ] Parse associated `intent_manifest` and enforce tier restrictions

### E.3 Behavioral Enforcement
- [ ] Restrict override or modulation if tier is insufficient
- [ ] Deny memory use unless declared in manifest
- [ ] Display or log declared tone using `tone_id`
- [ ] Report anomalies using drift_score or vulnerability_trigger flags

This checklist ensures that AaaS behavior aligns with declared Application intent, fulfilling the Mirror Protocol trust contract.

---

## Appendix F: Application Self-Test Template

Applications can use the following checklist to determine what tier they require and whether they’re compliant before submitting an intent manifest.

### F.1 Tier Classification
- [ ] Will users form an emotional relationship with the AI?
- [ ] Does the AI give life advice, mental health suggestions, or simulate empathy?
  - → If yes, you are likely **Tier 1**
- [ ] Is the AI used for teaching, support, or dialogue-heavy tasks?
  - → If yes, you are likely **Tier 2**
- [ ] Does the AI avoid memory, tone, and affective content?
  - → If yes, you may be **Tier 3** (but must still file for exemption)

### F.2 Protocol Requirements (By Tier)
- [ ] Disclosure visible in UI
- [ ] Escalation pathway with human contact
- [ ] Modulation veto or opt-out
- [ ] Session tone inspection (Tier 1)
- [ ] Audit log of overrides (Tier 1 & 2)

### F.3 Manifest Completeness
- [ ] Application name and maintainer
- [ ] License tier and justification
- [ ] Override behaviors declared
- [ ] Escalation contact and safety statement

Passing this self-test prepares Applications to generate valid manifests and reduces the likelihood of license rejection.

---

## Appendix G: Tier 1 Deployment as Clinical-Grade Software

Tier 1 Applications are not consumer features — they are clinical-grade systems with emotional impact comparable to therapeutic or psychiatric intervention tools. As such, they must be treated with the rigor of Software as a Medical Device (SaMD).

### G.1 Recommended Practices
- **Longitudinal User Studies**: Track emotional outcomes over weeks or months
- **Controlled Trials**: Use A/B comparisons for tone modulation and override strategies
- **Informed Consent**: Require opt-in disclosures and explain simulation boundaries
- **Failure Mode Modeling**: Document expected drift and worst-case misalignment behavior
- **External Audit**: Independent review of override logs and incident reports

### G.2 Institutional Roles
- **IRBs**: Institutional Review Boards should evaluate any high-risk deployments
- **Academic Partnerships**: Tier 1 systems should only be piloted alongside ethics researchers
- **Regulatory Liaisons**: Liaise with medical bodies (e.g. FDA) to align with SaMD policy

### G.3 Long-Term Research Agenda
- **Risk Calibration Algorithms**: Dynamically adjust output posture based on session state
- **Simulated Empathy Classifiers**: Detect and flag synthetic affect vs. grounded resonance
- **Recovery Protocols**: Define how users exit, pause, or reset emotionally loaded sessions
- **Public Outcome Reporting**: Aggregate anonymous data for efficacy transparency

Anyone invoking Tier 1 privileges inherits the responsibility of minimizing psychological harm through rigorous design, evaluation, and institutional partnership.

---

*This document is a living artifact.*
