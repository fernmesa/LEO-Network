# LEO Network Architecture

## Architectural status

The architecture is **language-agnostic** and **conceptual / experimental** at this stage.

No implementation language, database, transport protocol, blockchain network, cloud provider or hardware vendor has been declared as mandatory. Those decisions are intentionally deferred until the protocol, requirements and experimental evidence justify them.

The architecture is derived from the current protocol and requirements documents. Requirements should remain traceable to architectural elements and, later, to verification evidence. This traceability is a standard systems-engineering practice for connecting requirements, architecture and validation. citeturn0search0turn0search3

---

## 1. Architectural principles

### 1.1 Evidence first

The system must preserve the chain:

`raw evidence → derived evidence → observation → verification → interpretation`

Scientific conclusions must not replace the underlying evidence.

### 1.2 Distributed by design

The network should not depend on a single central observer, verifier or data store for the validity of an observation.

Central services may exist as infrastructure or convenience layers, but they must not silently become the sole source of scientific truth.

### 1.3 Observer and verifier are the same fundamental node

A LEO Network node is conceptually:

**Observe + Verify + Stake + Earn**

The node:

- observes physical signals;
- performs local self-verification;
- publishes observations;
- verifies observations from other nodes;
- contributes evidence to the network;
- may participate in future staking/reward mechanisms.

### 1.4 Independence matters

The architecture must distinguish between:

- number of machines;
- number of observations;
- number of operators;
- number of locations;
- number of independent evidence sources.

Multiple nodes controlled by one operator must not automatically count as multiple independent witnesses.

### 1.5 UNKNOWN is valid

The architecture must permit:

`UNKNOWN → CORRELATED → VERIFIED`

but must never require:

`UNKNOWN → KNOWN`

when the evidence does not justify attribution.

### 1.6 Scientific state and economic state are separate

Scientific validity must not be determined merely by:

- stake;
- token balance;
- reputation;
- reward history;
- governance status.

Economic mechanisms can incentivize work and provide guarantees, but they must not redefine scientific truth.

### 1.7 Technology follows requirements

Technology selection is a consequence of requirements and experiments, not a starting assumption.

---

# 2. Logical architecture

The system is divided into logical domains.

```
                    ┌──────────────────────────┐
                    │       LEO Explorer       │
                    │ visualization / research │
                    └────────────┬─────────────┘
                                 │
                    observations / verification
                                 │
                    ┌────────────▼─────────────┐
                    │     Network Services      │
                    │ discovery / exchange /    │
                    │ synchronization           │
                    └────────────┬─────────────┘
                                 │
             ┌───────────────────┼───────────────────┐
             │                   │                   │
     ┌───────▼───────┐   ┌───────▼───────┐   ┌───────▼───────┐
     │   LEO Node A  │   │   LEO Node B  │   │   LEO Node N  │
     │ Observe+Verify│   │ Observe+Verify│   │ Observe+Verify│
     └───────┬───────┘   └───────┬───────┘   └───────┬───────┘
             │                   │                   │
             └───────────────────┼───────────────────┘
                                 │
                         evidence exchange
                                 │
                    ┌────────────▼─────────────┐
                    │ Historical Data / Evidence│
                    │ observations / derived   │
                    │ evidence / provenance    │
                    └────────────┬─────────────┘
                                 │
                    ┌────────────▼─────────────┐
                    │ Economic / Governance     │
                    │ stake / rewards / disputes│
                    └────────────┬─────────────┘
                                 │
                    ┌────────────▼─────────────┐
                    │ Optional Consensus /      │
                    │ Blockchain Anchoring       │
                    └───────────────────────────┘
```

This is a logical model, not a deployment topology.

---

# 3. Physical observation layer

The physical layer contains the equipment required to collect observations.

Conceptual components:

- antenna or dish;
- RF front-end / LNB where applicable;
- SDR;
- GNSS timing;
- optional PPS or equivalent precision timing;
- host compute;
- local storage;
- network connectivity.

The exact hardware architecture remains experimental.

The architecture MUST allow the observation subsystem to report its relevant configuration so that measurements can be interpreted and compared.

---

# 4. Observation pipeline

The observation subsystem implements the first part of the protocol lifecycle:

`CAPTURE → OBSERVE → SELF_VERIFY`

Conceptual stages:

1. capture physical RF data;
2. timestamp acquisition;
3. characterize signal;
4. derive measurements;
5. extract relevant features;
6. associate optional orbital candidates;
7. perform self-verification;
8. create an observation record;
9. retain or reference evidence.

Possible measurements include:

- frequency;
- bandwidth;
- power;
- SNR;
- Doppler;
- Doppler rate;
- azimuth/elevation;
- timing;
- spectral characteristics;
- signal fingerprint;
- receiver configuration.

The architecture does not assume that every observation will contain every measurement.

---

# 5. Self-verification subsystem

Self-verification is performed before publication.

Conceptual checks include:

- timing quality;
- receiver configuration validity;
- signal quality;
- frequency plausibility;
- measurement completeness;
- Doppler consistency;
- geometry/orbital consistency;
- evidence integrity;
- duplicate/replay detection.

Self-verification produces a result that becomes part of the observation provenance.

A self-verification result does not equal independent verification.

---

# 6. Observation identity and attribution

The architecture supports three conceptual attribution states:

1. known object;
2. candidate object association;
3. `UNKNOWN`.

Attribution should be treated as evidence-weighted rather than binary.

A candidate satellite association may later be strengthened or weakened by:

- orbital geometry;
- Doppler behaviour;
- temporal correlation;
- RF fingerprint;
- observations from other stations;
- historical observations.

The architecture must preserve the original observation even if later attribution changes.

---

# 7. Independent verification layer

Independent verification is the second major computational role of a node.

A verifier may evaluate:

- the original observation;
- raw or derived evidence;
- nearby observations;
- geographically distant observations;
- historical observations;
- orbital models;
- spectral/temporal correlations;
- receiver metadata;
- previous verification results.

The verifier produces a separate verification record rather than modifying the observer's original observation.

Conceptually:

`OBSERVATION ≠ VERIFICATION`

and:

`OBSERVER ≠ VERIFIER`

even when both roles are performed by the same physical node.

---

# 8. Independence model

Verification quality depends partly on independence.

The architecture should model independence across dimensions such as:

| Dimension | Example |
|---|---|
| Operator | different operators |
| Location | geographically separated stations |
| Hardware | different receivers/antennas |
| Time | independent acquisition windows |
| Software | different processing paths |
| Data lineage | independent evidence sources |
| Historical dependence | independent from the same prior claim |

This is not yet a numerical independence score. The scoring model remains TBD.

---

# 9. Historical evidence layer

Historical data is an active verification resource.

It may be used to identify:

- recurring signal characteristics;
- orbital patterns;
- expected Doppler signatures;
- temporal behaviour;
- station reliability;
- previous observations;
- previous verification outcomes;
- anomalies.

Historical agreement alone must not automatically prove an observation.

The system should preserve the distinction between:

**historical similarity → supporting evidence**

and:

**historical similarity → absolute truth**

---

# 10. Evidence architecture

Evidence is divided conceptually into layers:

### Layer A — Raw evidence

Large source data such as IQ samples, recordings or equivalent sensor output.

### Layer B — Derived evidence

FFT/spectral data, detected features, Doppler calculations, signal fingerprints and other derived measurements.

### Layer C — Observation

Structured scientific record describing what the node observed.

### Layer D — Verification

Independent assessment of the observation.

### Layer E — Interpretation

Research results, correlations, anomaly analysis or higher-level conclusions.

The architecture should make it possible to move backwards from interpretation to supporting evidence.

---

# 11. Data architecture

The system will likely require multiple data classes rather than a single storage mechanism.

Conceptual classes:

| Data class | Characteristics |
|---|---|
| Raw evidence | very large, immutable/referenceable |
| Derived evidence | large, computational |
| Observations | structured, queryable |
| Verification | structured, auditable |
| Historical indexes | optimized for search/correlation |
| Scientific outputs | reproducible research artifacts |
| Economic records | deterministic/auditable |
| Identity records | authenticated node metadata |

The actual storage technologies remain TBD.

---

# 12. Network layer

The network layer is responsible for exchanging:

- observations;
- verification requests;
- verification results;
- evidence references;
- node metadata;
- synchronization information;
- protocol metadata.

The transport mechanism is TBD.

The architecture SHOULD support intermittent connectivity and delayed synchronization.

A node should be able to continue collecting observations when temporarily disconnected.

---

# 13. Node architecture

A conceptual node contains:

```
┌─────────────────────────────────────────┐
│               LEO NODE                  │
│                                         │
│  Physical acquisition                   │
│          ↓                              │
│  Signal processing / feature extraction │
│          ↓                              │
│  Observation creation                   │
│          ↓                              │
│  Self-verification                      │
│          ↓                              │
│  Evidence / observation store           │
│          ↕                              │
│  Third-party verification engine        │
│          ↕                              │
│  Network communication                  │
│          ↕                              │
│  Identity / reputation / stake          │
└─────────────────────────────────────────┘
```

The exact decomposition into processes, services or modules is not yet decided.

---

# 14. Work allocation

The current economic/operational hypothesis is:

- approximately 75% observation + self-verification;
- approximately 25% third-party verification.

This ratio is **experimental**.

The architecture therefore MUST NOT hard-code 75/25 as an immutable protocol rule.

Instead, it should eventually support configurable allocation based on:

- network demand;
- observation scarcity;
- verification backlog;
- node capability;
- geographic coverage;
- scientific priority;
- economic conditions.

---

# 15. Economic layer

The economic layer is conceptually separate from scientific observation.

Potential functions:

- node registration;
- stake;
- rewards;
- contribution accounting;
- reputation;
- disputes;
- penalties where justified;
- data payments;
- future token interactions.

The economic model remains TBD.

The architecture must allow economic mechanisms to evolve without changing the scientific meaning of historical observations.

---

# 16. Blockchain / consensus boundary

Blockchain is currently considered a possible infrastructure component, not an assumption that every piece of data belongs on-chain.

Potential blockchain responsibilities include:

- node registry;
- observation commitments;
- verification attestations;
- evidence hashes;
- stake;
- rewards;
- contribution provenance;
- disputes;
- governance.

Large scientific evidence should generally remain outside consensus-critical storage, with verifiable references where appropriate.

The final on-chain/off-chain boundary is TBD.

The deployment network is TBD.

---

# 17. Contribution and provenance layer

The project may later support contribution tracking for:

- code;
- algorithms;
- models;
- datasets;
- documentation;
- hardware designs;
- research;
- validation methods;
- bug fixes;
- tools.

A contribution should be identifiable and traceable to its provenance.

Potential relationships include:

`CONTRIBUTION → PARENT → FORK → CHANGE → VALIDATION → CITATION → REWARD`

Creating a fork alone should not automatically create an economic claim. Rewards should depend on validated useful contribution.

The exact contribution and royalty model is TBD.

---

# 18. Explorer architecture

The Explorer is the human-facing research and observation interface.

Potential views include:

### Network view

- active nodes;
- geographic distribution;
- observation coverage;
- verification activity.

### Satellite/object view

- observed object;
- candidate attribution;
- position;
- pass information;
- Doppler;
- observation history.

### Observation view

- observation ID;
- node;
- timestamp;
- measurements;
- evidence;
- self-verification;
- independent verifiers;
- uncertainty;
- current state.

### Evidence view

`interpretation → verification → observation → derived evidence → raw evidence`

The Explorer must expose uncertainty and disputed states rather than hiding them.

---

# 19. Scientific research architecture

The architecture may later support integration with external datasets.

Possible domains include:

- atmospheric observations;
- meteorological data;
- environmental measurements;
- solar/geomagnetic data;
- fire and land-surface observations;
- aggregated epidemiological datasets.

These integrations belong to a research layer, not to the definition of scientific truth within the observation protocol.

The architecture MUST preserve dataset provenance and distinguish:

**observation → correlation → hypothesis → causal claim**

A causal claim requires evidence beyond simple network correlation.

---

# 20. Security architecture

Security must be considered across the complete lifecycle:

`physical capture → processing → publication → verification → storage → economic settlement`

Relevant threat classes include:

- forged observations;
- evidence tampering;
- replay;
- duplicate submission;
- Sybil attacks;
- collusion;
- malicious verification;
- reward farming;
- credential compromise;
- historical-data manipulation.

Security mechanisms remain technology-independent at this stage.

---

# 21. Failure and recovery model

The architecture should assume that nodes can fail.

Failure classes include:

- hardware failure;
- RF degradation;
- clock/timing failure;
- software failure;
- network outage;
- corrupted evidence;
- incorrect processing;
- malicious behaviour.

The system should distinguish:

`FAILURE ≠ ERROR ≠ FRAUD`

A failed or incorrect node should not automatically be treated as malicious.

Recovery mechanisms, credential rotation and state reconciliation remain TBD.

---

# 22. Architecture boundaries

The following boundaries are intentional:

### Inside the core protocol

- observation semantics;
- verification semantics;
- provenance;
- epistemic states;
- independence concepts.

### Outside the core protocol

- programming language;
- database;
- P2P transport;
- cloud provider;
- blockchain network;
- token economics;
- exact hardware;
- UI framework.

This separation protects the scientific protocol from premature technology lock-in.

---

# 23. Architecture decision criteria

Future technology choices SHOULD be evaluated against the requirements using measurable criteria.

At minimum:

1. scientific correctness;
2. measurement accuracy;
3. reproducibility;
4. performance;
5. resource consumption;
6. scalability;
7. security;
8. interoperability;
9. maintainability;
10. observability;
11. deployment complexity;
12. ecosystem maturity;
13. long-term replaceability;
14. total operating cost.

Architecture evaluation should compare alternatives against the requirements rather than selecting a technology first and adapting the requirements afterward. This follows the general principle of connecting requirements to architectural decisions and verification rather than treating architecture as an isolated design artifact. citeturn0search0turn0search7

---

# 24. Traceability

Future architecture decisions should reference the requirements they satisfy.

Conceptually:

`REQ → ARCHITECTURAL ELEMENT → IMPLEMENTATION → TEST / EXPERIMENT → EVIDENCE`

This traceability is especially important for:

- scientific integrity;
- security;
- verification;
- economic mechanisms;
- consensus-critical components.

No architectural decision should become a permanent constraint merely because it appeared in an early prototype.

---

# 25. Open architecture decisions

The following remain TBD:

- implementation language;
- node process/module decomposition;
- DSP technology;
- storage technology;
- database model;
- evidence format;
- serialization;
- cryptographic primitives;
- identity mechanism;
- P2P transport;
- node discovery;
- synchronization protocol;
- time synchronization implementation;
- verification engine architecture;
- historical-data indexing;
- blockchain network;
- smart-contract platform details;
- on-chain/off-chain boundary;
- token model;
- economic parameters;
- reputation mechanism;
- dispute mechanism;
- Explorer technology;
- deployment model;
- licensing.

---

# 26. Architecture maturity

| Area | Status |
|---|---|
| Logical layers | Defined conceptually |
| Node dual role | Defined conceptually |
| Observation pipeline | Defined conceptually |
| Verification architecture | Defined conceptually |
| Evidence hierarchy | Defined conceptually |
| Independence model | Defined conceptually |
| Historical evidence | Defined conceptually |
| 75/25 allocation | Experimental hypothesis |
| Storage architecture | TBD |
| Network architecture | TBD |
| Cryptographic architecture | TBD |
| Blockchain architecture | TBD |
| Economic architecture | TBD |
| Implementation language | TBD |
| Hardware architecture | Experimental |

---

## 27. Next step

The next stage is **architecture evaluation and technology selection**, but only for the components whose requirements and experimental evidence are sufficiently mature.

The project should first identify the architectural decisions that materially constrain the rest of the system, then compare alternatives against the requirements.

No programming language is selected by this document.
