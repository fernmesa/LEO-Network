# LEO Network Requirements

**Status:** Conceptual / experimental  
**Scope:** System-level requirements derived from the current protocol specification  
**Implementation language:** Not declared  
**Technology choices:** Not declared

---

## 1. Purpose

This document defines the requirements that the LEO Network should satisfy before implementation decisions are made.

Requirements are deliberately separated from implementation technologies. A requirement describes **what the system must achieve**; it does not prescribe how it must be implemented.

The requirements are derived from the current protocol model:

`CAPTURE → OBSERVE → SELF_VERIFY → PUBLISH → INDEPENDENT_VERIFY → STATE`

No requirement in this document should be interpreted as proof that the underlying scientific or economic assumptions have already been validated.

---

## 2. Requirement levels

The following terms are normative:

- **MUST** — required for protocol or system validity.
- **SHOULD** — strongly recommended unless a documented reason exists not to implement it.
- **MAY** — optional capability.
- **TBD** — decision not yet defined.
- **EXPERIMENTAL** — hypothesis requiring empirical validation.

---

## 3. Scientific integrity requirements

### REQ-SCI-001 — Evidence provenance
The system MUST preserve the provenance of an observation from captured evidence through derived measurements, observation records, verification results and later interpretations.

### REQ-SCI-002 — Uncertainty
Measurements and derived results SHOULD expose uncertainty or confidence information whenever meaningful.

### REQ-SCI-003 — UNKNOWN identity
The system MUST allow an observation to remain `UNKNOWN` when available evidence does not justify an identification.

### REQ-SCI-004 — No forced attribution
The system MUST NOT require an observation to be associated with a known satellite merely because a candidate exists.

### REQ-SCI-005 — Correlation distinction
The system MUST distinguish observational correlation from causal interpretation.

### REQ-SCI-006 — Reproducibility
A published observation SHOULD contain enough metadata and references to permit independent reproduction or audit of the processing path, subject to evidence-size and privacy constraints.

### REQ-SCI-007 — Model transparency
Models used for orbital, RF, signal or statistical verification SHOULD be identifiable by version or equivalent immutable reference.

---

## 4. Observation requirements

### REQ-OBS-001 — Timestamp
Every observation MUST contain a trustworthy timestamp or explicitly declare that timing quality is unknown.

### REQ-OBS-002 — Node identity
Every observation MUST identify the observing node.

### REQ-OBS-003 — Receiver context
An observation MUST record sufficient receiver/configuration context to interpret its measurements.

### REQ-OBS-004 — Measurement data
The observation SHOULD support frequency, bandwidth, signal-quality measurements, Doppler-related measurements and relevant geometry.

### REQ-OBS-005 — Evidence reference
An observation MUST reference the underlying evidence or a verifiable representation of it.

### REQ-OBS-006 — Integrity
Published evidence and observation metadata MUST provide a mechanism for detecting alteration or substitution.

### REQ-OBS-007 — Duplicate protection
The system MUST provide mechanisms to detect replayed, duplicated or otherwise reused observations.

---

## 5. Self-verification requirements

### REQ-SELF-001 — Local validation
A node MUST be capable of evaluating its own observation before publication.

### REQ-SELF-002 — Time validation
Self-verification SHOULD evaluate clock synchronization and timing quality.

### REQ-SELF-003 — Signal validation
Self-verification SHOULD evaluate signal quality, frequency plausibility and measurement completeness.

### REQ-SELF-004 — Geometry validation
Where sufficient data exists, self-verification SHOULD evaluate consistency with expected geometry and orbital behaviour.

### REQ-SELF-005 — Evidence validation
The node MUST verify that the evidence referenced by its observation is complete enough for the declared observation state.

---

## 6. Independent verification requirements

### REQ-VER-001 — Independent verification
An observation MUST be capable of receiving verification from entities other than its originating node.

### REQ-VER-002 — Independence metadata
Verification SHOULD record relevant independence dimensions, including operator, location, hardware, timing, software/data lineage and evidence provenance.

### REQ-VER-003 — Multi-source evidence
The verification system SHOULD support combining geographically and temporally independent observations.

### REQ-VER-004 — Historical evidence
Historical observations SHOULD be usable as verification evidence.

### REQ-VER-005 — Model-based verification
Orbital, temporal, spectral and other validated models MAY contribute to verification.

### REQ-VER-006 — Confidence
Verification results SHOULD expose confidence and/or uncertainty rather than presenting uncertain conclusions as absolute facts.

### REQ-VER-007 — Conflicting evidence
The system MUST preserve conflicting verification results rather than silently replacing them.

---

## 7. Epistemic state requirements

### REQ-STATE-001 — Explicit states
The system MUST support explicit states for observations and verification outcomes.

At minimum, the protocol SHOULD support:

- UNKNOWN
- OBSERVED
- SELF_VERIFIED
- CORRELATED
- VERIFIED
- DISPUTED
- INCONSISTENT
- ERROR
- FRAUD_DEMONSTRATED

### REQ-STATE-002 — State provenance
Every state transition MUST be attributable to a defined observation, verification, rule or event.

### REQ-STATE-003 — Error versus fraud
Ordinary measurement, hardware or algorithmic error MUST NOT automatically be classified as fraud.

### REQ-STATE-004 — Fraud evidence
A `FRAUD_DEMONSTRATED` state MUST require evidence satisfying explicitly defined protocol rules.

---

## 8. Network node requirements

### REQ-NODE-001 — Dual role
A network node SHOULD support both observation and verification.

### REQ-NODE-002 — Self-verification
A node MUST be able to self-verify observations that it publishes.

### REQ-NODE-003 — Third-party verification
A node SHOULD be able to verify observations originating from other nodes.

### REQ-NODE-004 — Work allocation
The network SHOULD support configurable allocation between own observation and third-party verification.

### REQ-NODE-005 — Provisional 75/25 model
The current concept assumes approximately 75% observation/self-verification and 25% third-party verification as an experimental starting point. This is NOT a final protocol parameter.

### REQ-NODE-006 — Independence
The network MUST distinguish node identity from independent observation identity. Multiple nodes controlled by one operator MUST NOT automatically count as independent witnesses.

---

## 9. Data and evidence requirements

### REQ-DATA-001 — Layered data
The system SHOULD distinguish at least:

1. raw evidence,
2. derived evidence,
3. observation records,
4. verification records,
5. interpretation or research outputs.

### REQ-DATA-002 — Large evidence
Large binary evidence SHOULD be stored outside consensus-critical records when appropriate, while retaining verifiable references and integrity information.

### REQ-DATA-003 — Metadata integrity
Metadata required to interpret evidence MUST be preserved with the evidence reference.

### REQ-DATA-004 — Historical query
The system SHOULD support querying historical observations by relevant dimensions such as time, location, object, signal characteristics and verification state.

### REQ-DATA-005 — Research reuse
Data SHOULD be reusable for scientific analysis without requiring the original observer to approve every legitimate research query, subject to future governance, privacy and access rules.

---

## 10. Security requirements

### REQ-SEC-001 — Identity integrity
The system MUST provide a mechanism for authenticating node-originated records.

### REQ-SEC-002 — Evidence integrity
The system MUST provide a mechanism to detect tampering with published evidence references and records.

### REQ-SEC-003 — Replay resistance
The protocol MUST mitigate replay and duplicate-submission attacks.

### REQ-SEC-004 — Sybil resistance
The economic and/or protocol layers MUST address attempts to create artificial identities to gain disproportionate influence or rewards.

### REQ-SEC-005 — Collusion
The verification model SHOULD account for collusion between nodes, operators or data sources.

### REQ-SEC-006 — Economic attack resistance
Any future staking or reward mechanism MUST consider manipulation, false verification, reward farming and other incentive attacks.

### REQ-SEC-007 — Recovery
Nodes SHOULD have a defined recovery process for loss of local state, credentials or connectivity.

---

## 11. Economic requirements

These requirements describe the intended economic behaviour without deciding the final token or monetary model.

### REQ-ECO-001 — Useful work
Any future reward mechanism SHOULD compensate useful, verifiable contribution rather than raw activity volume.

### REQ-ECO-002 — Observation rewards
The economic model MAY reward useful observations.

### REQ-ECO-003 — Verification rewards
The economic model MAY reward useful independent verification.

### REQ-ECO-004 — Quality weighting
Rewards SHOULD account for quality, utility, novelty, independence, coverage and verifiability.

### REQ-ECO-005 — Anti-spam
The reward mechanism MUST resist low-value or duplicated submissions designed primarily to extract rewards.

### REQ-ECO-006 — Error handling
Normal scientific or hardware error SHOULD be handled differently from demonstrated intentional fraud.

### REQ-ECO-007 — Sustainability
Before production economic deployment, the project MUST measure the relationship between node operating cost, useful work, data demand and sustainable rewards.

### REQ-ECO-008 — Token decision
Token existence, type, supply, issuance, inflation/deflation, burning and utility remain TBD.

---

## 12. Governance and disputes

### REQ-GOV-001 — Rule transparency
Verification and reward rules SHOULD be publicly documented.

### REQ-GOV-002 — Dispute process
The system MUST define a mechanism for disputed observations or verification results before production deployment.

### REQ-GOV-003 — Evidence-based decisions
Dispute resolution SHOULD operate on recorded evidence, provenance and protocol rules.

### REQ-GOV-004 — Economic penalties
Any future penalty or slashing mechanism MUST distinguish demonstrated misconduct from ordinary measurement error.

### REQ-GOV-005 — Governance separation
Governance mechanisms MUST NOT be allowed to silently alter historical scientific evidence.

---

## 13. Performance and availability

### REQ-PERF-001 — Local operation
A node SHOULD be capable of collecting and processing observations without continuous dependence on a central server.

### REQ-PERF-002 — Intermittent connectivity
The system SHOULD tolerate temporary network disconnection and synchronize later.

### REQ-PERF-003 — Evidence ingestion
The architecture MUST support substantially larger evidence volumes than consensus-critical metadata.

### REQ-PERF-004 — Queryability
Historical observations and verification results SHOULD remain efficiently queryable as the network grows.

### REQ-PERF-005 — Scalability
The architecture SHOULD allow additional nodes, observation volume and research consumers without requiring a redesign of the scientific protocol.

---

## 14. Privacy and legal requirements

### REQ-PRIV-001 — Data minimization
The system SHOULD avoid publishing personal information that is not necessary for scientific or protocol purposes.

### REQ-PRIV-002 — Operator identity
The protocol SHOULD distinguish public node identity from private operator identity where legally and technically appropriate.

### REQ-PRIV-003 — Location sensitivity
The project MUST explicitly assess whether exact node location can create privacy or security risks before publication.

### REQ-PRIV-004 — Legal compliance
Deployment requirements MUST account for applicable radio, telecommunications, data protection and other relevant laws in each operating jurisdiction.

---

## 15. Research and environmental data

The network MAY later integrate external datasets for scientific research, including atmospheric, meteorological, environmental, solar/geomagnetic and other datasets.

### REQ-RES-001 — External provenance
External datasets MUST retain source and version/provenance information.

### REQ-RES-002 — Correlation analysis
Research tooling SHOULD support correlation and statistical analysis without presenting correlation as established causation.

### REQ-RES-003 — Confounders
Research conclusions SHOULD document relevant confounders and limitations.

### REQ-RES-004 — Reproducibility
Published research results SHOULD reference the datasets, processing methods and relevant model versions required for reproduction.

### REQ-RES-005 — Health-related research
Any research involving health or epidemiological outcomes MUST apply appropriate scientific, statistical, ethical and privacy safeguards. The network MUST NOT represent observational correlations as medical causation.

---

## 16. Explorer / user-facing requirements

### REQ-UI-001 — Observation visibility
A user-facing explorer SHOULD allow users to inspect observations and their verification state.

### REQ-UI-002 — Satellite/pass context
Where sufficient data exists, the explorer SHOULD provide orbital/pass context.

### REQ-UI-003 — Evidence traceability
Users SHOULD be able to trace a displayed result back to its observation, verification records and evidence references.

### REQ-UI-004 — Uncertainty visibility
The interface SHOULD expose uncertainty and disputed/inconsistent states instead of hiding them.

### REQ-UI-005 — Network visibility
The explorer MAY display node participation, verification activity, stake and reputation once those mechanisms are experimentally validated.

---

## 17. Implementation independence

### REQ-IMP-001 — Language independence
The requirements MUST remain implementable without depending on a specific programming language.

### REQ-IMP-002 — Technology independence
The requirements MUST remain implementable without prematurely selecting a database, blockchain, transport protocol, hardware vendor or cloud provider.

### REQ-IMP-003 — Replaceability
Core scientific and protocol semantics SHOULD remain portable across future implementation technologies.

---

## 18. Validation gates

No production implementation should be considered justified solely because these requirements have been written.

Before moving to production architecture, the project SHOULD validate at least:

1. whether the proposed hardware can reliably observe the target phenomena;
2. whether timestamps, frequency measurements and Doppler measurements are sufficiently accurate;
3. whether self-verification can reject meaningful classes of bad observations;
4. whether independent nodes can actually provide useful verification;
5. whether historical data improves verification quality;
6. whether independence can be measured in practice;
7. whether the provisional 75/25 workload model is operationally realistic;
8. whether useful work can be measured objectively;
9. whether the economic model can sustain real nodes;
10. whether the scientific value justifies the operational cost.

These are validation objectives, not assumed results.

---

## 19. Open requirements decisions

The following remain deliberately unresolved:

- Exact observation schema: TBD
- Canonical identifiers: TBD
- Evidence serialization: TBD
- Cryptographic mechanism: TBD
- Time synchronization requirements: TBD
- Verification quorum/threshold: TBD
- Node discovery: TBD
- Transport mechanism: TBD
- Storage architecture: TBD
- On-chain/off-chain boundary: TBD
- Reputation model: TBD
- Dispute mechanism: TBD
- Economic model: TBD
- Token model: TBD
- Deployment network: TBD
- Implementation language: TBD
- Project license: TBD

---

## 20. Requirement status

| Area | Status |
|---|---|
| Scientific principles | Conceptually defined |
| Observation lifecycle | Conceptually defined |
| Verification model | Conceptually defined |
| Error/fraud distinction | Conceptually defined |
| Node dual-role model | Conceptually defined |
| 75/25 allocation | Experimental hypothesis |
| Economic model | TBD |
| Token | TBD |
| Blockchain/deployment network | TBD |
| Implementation language | TBD |
| Hardware specification | Experimental |
| Exact data schema | TBD |
| Cryptographic mechanisms | TBD |
| Production security model | TBD |

---

## 21. Next step

The next design stage is **technical architecture**.

Only after these requirements have been reviewed and experimentally validated should the project compare candidate technologies for:

- node software,
- signal/data processing,
- storage,
- networking,
- cryptography,
- distributed coordination,
- explorer,
- and eventual economic/blockchain infrastructure.

No implementation language is selected by this document.
