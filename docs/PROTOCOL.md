# LEO Network Protocol

## Status

**Protocol specification — conceptual / experimental.**

This document defines the current protocol model without prescribing an implementation language, transport, database, blockchain or hardware vendor.

## Core lifecycle

`CAPTURE → OBSERVE → SELF_VERIFY → PUBLISH → INDEPENDENT_VERIFY → STATE`

The lifecycle is intentionally separated from implementation details.

## Observation

An observation represents a claim backed by physical measurement and evidence.

A conceptual observation record should contain, at minimum:

| Field | Purpose |
|---|---|
| Observation ID | Globally unique reference |
| Node ID | Originating observation node |
| Timestamp | Measurement time |
| Position | Approximate observer location |
| Receiver configuration | Hardware/configuration context |
| Frequency | Observed RF frequency |
| Bandwidth | Observed signal bandwidth |
| Signal metrics | Power, SNR and related measurements |
| Doppler | Doppler shift and, when available, Doppler rate |
| Geometry | Azimuth/elevation and orbital context when available |
| Signal features | Spectral and RF fingerprint features |
| Evidence reference | Reference to raw/derived evidence |
| Evidence hash | Integrity commitment |
| Processing metadata | Processing/model/configuration information |
| Initial state | State assigned by the protocol |

The exact serialization format remains **TBD**.

## Observation identity

An observation is identified by its protocol identity and evidence provenance, not solely by a claimed satellite identity.

A node may publish:

- a known object association;
- a candidate association;
- or `UNKNOWN`.

`UNKNOWN` must remain a valid outcome throughout verification.

## Self-verification

Before publication, the observing node should perform local checks including, where applicable:

1. timestamp and clock synchronization;
2. receiver configuration validity;
3. signal quality;
4. frequency plausibility;
5. Doppler plausibility;
6. geometric/orbital consistency;
7. evidence completeness;
8. evidence integrity;
9. duplicate/replay detection.

Self-verification does not make an observation independently verified.

## Independent verification

Third-party verification should use evidence that is meaningfully independent from the original observation.

Relevant independence dimensions include:

- operator;
- physical location;
- hardware;
- acquisition time;
- software/data lineage;
- evidence source;
- historical dependence.

Multiple machines controlled by the same operator must not automatically count as multiple independent witnesses.

Verification may combine:

- nearby observations;
- geographically distant observations;
- orbital models;
- historical observations;
- RF fingerprints;
- temporal correlation;
- spectral correlation;
- cross-station consistency;
- other scientifically justified evidence.

## Verification result

A verifier should produce a signed/traceable verification result containing:

- verifier identity;
- observation reference;
- verification timestamp;
- checks performed;
- evidence references used;
- result;
- confidence/uncertainty where applicable;
- protocol or model information;
- verifier stake/reputation context where applicable.

The exact signature and serialization mechanisms are **TBD**.

## Epistemic states

Possible states include:

- `UNKNOWN`
- `OBSERVED`
- `SELF_VERIFIED`
- `CORRELATED`
- `VERIFIED`
- `DISPUTED`
- `INCONSISTENT`
- `ERROR`
- `FRAUD_DEMONSTRATED`

These states describe the status of evidence and claims. They must not be interpreted as certainty beyond the evidence available.

## Error versus fraud

A failed measurement, disagreement or algorithmic mistake is not automatically fraudulent.

Potential states should distinguish:

- measurement error;
- incomplete evidence;
- inconsistent observations;
- unresolved dispute;
- protocol violation;
- demonstrated malicious behaviour.

Penalties or slashing require explicit protocol conditions and evidence sufficient under those conditions. The protocol must not equate ordinary scientific uncertainty with fraud.

## Historical correlation

Historical observations are active verification evidence.

The historical layer may be used to evaluate:

- recurrence;
- orbital consistency over time;
- signal fingerprints;
- expected pass behaviour;
- station reliability;
- anomaly detection;
- duplicate observations;
- prior verification outcomes.

Historical agreement is evidence, not proof by itself.

## Evidence model

Large scientific payloads such as IQ recordings, FFTs and spectrograms should normally remain off-chain or outside the consensus layer.

The protocol should preserve:

`raw evidence → derived evidence → observation → verification → interpretation`

Each transformation should be traceable through hashes, metadata and processing information where practical.

## Anti-replay and anti-duplication

The protocol should detect or limit:

- replayed observations;
- duplicated evidence;
- copied observations presented as independent measurements;
- fabricated timestamps;
- repeated submissions with no additional information.

Exact detection rules remain **TBD** and should be tested against legitimate repeated observations.

## Economic interaction

The protocol may later connect observation and verification to:

- rewards;
- stake;
- reputation;
- contribution history;
- disputes;
- penalties.

Economic parameters are not part of the finalized observation semantics yet.

## Protocol invariants

The following are intended as foundational invariants:

1. An observation does not become verified solely because its origin node says so.
2. `UNKNOWN` is always a valid result.
3. Independence must be evaluated explicitly.
4. Evidence provenance must be preserved.
5. Correlation must not be presented as causation.
6. Scientific error must not automatically be treated as fraud.
7. Large evidence does not need to be stored on-chain to be verifiable.
8. Protocol semantics must remain independent of implementation language.
9. Economic incentives must not redefine scientific truth.
10. No production deployment should be treated as justified until the physical and verification assumptions are experimentally tested.

## Open protocol decisions

The following remain **TBD**:

- observation serialization format;
- canonical identifiers;
- cryptographic signature scheme;
- evidence storage protocol;
- P2P transport;
- node discovery;
- time synchronization requirements;
- verification quorum/threshold rules;
- reputation calculation;
- dispute procedure;
- on-chain/off-chain boundary;
- final economic parameters.

These decisions should be resolved through experiments, threat modelling and protocol review rather than assumptions.
