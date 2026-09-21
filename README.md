# LEO Network

**Distributed Observation, Verification and Scientific Data Network**

> Observe. Verify. Prove. Contribute.

LEO Network is an experimental open architecture for a distributed network of physical observation nodes capable of collecting, verifying, correlating and publishing evidence about low-Earth-orbit (LEO) objects and, potentially, other scientific phenomena.

## Status

**Concept / experimental design — not production ready.**

The architecture, protocol, economic model and token design are intentionally incomplete. Real hardware measurements and simulations must precede production decisions.

## Core principles

- No single observer.
- No single validator.
- No single database as the only source of truth.
- Evidence before conclusions.
- `UNKNOWN` is a valid result.
- Correlation is not causation.
- Sensor error is not automatically fraud.
- Historical data is part of verification.
- Heavy scientific data stays off-chain; hashes and attestations can be anchored on-chain.
- Passive observation by design: measurement and analysis, not interference or control.

## The LEO Node

**LEO Node = Observe + Verify + Stake + Earn**

Each node can observe physical signals, perform local self-verification, verify observations from other nodes, maintain cryptographic provenance, stake value as an economic guarantee, and receive rewards for useful independently verifiable work.

The current conceptual workload target is approximately **75% observation/self-verification and 25% third-party verification**. The final protocol should make this parameter configurable.

## Observation

An observation may contain timestamp, station identity, geographic position, frequency, bandwidth, received power, SNR, Doppler shift, Doppler rate, azimuth/elevation, spectral features, RF fingerprint features, receiver configuration, orbital context and an evidence hash.

Raw IQ, FFTs, spectrograms and other large evidence should normally remain off-chain.

## Verification

Verification can combine signal-quality checks, time synchronization, orbital models such as TLE/SGP4, expected Doppler behaviour, historical observations, RF fingerprints, nearby and distant independent stations, and temporal/spectral correlation.

Independence is a protocol property. Ten machines controlled by one operator should not automatically count as ten independent witnesses.

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

An observation must never be forced into a satellite identity merely because an orbital model suggests one.

## Proof of Useful Observation

The economic concept is **Proof of Useful Observation (PoUO)**. Nodes should not earn simply by producing large amounts of data; rewards should depend on useful, verifiable contribution.

Conceptual reward function:

`REWARD = quality × utility × novelty × independence × coverage × verifiability`

This is a design hypothesis, not a finalized formula.

## Stake and veracity

Stake acts as a guarantee attached to claims or validation work. Correct independently verified work can earn rewards; ordinary sensor or algorithm errors should not automatically be treated as fraud; demonstrated protocol-defined fraud may result in penalties.

## Scientific data network

The architecture can extend beyond LEO observation to atmospheric, meteorological, fire, land-surface, solar/geomagnetic and other openly available scientific datasets.

The network should provide provenance, uncertainty, reproducibility and correlation tools.

**CORRELATION ≠ CAUSATION.**

## Blockchain

The current direction is an **EVM-compatible** architecture, with **Polygon** as the candidate ecosystem.

Candidate contracts include `LEOToken`, `NodeRegistry`, `ObservationRegistry`, `VerificationRegistry`, `SatelliteRegistry`, `EvidenceRegistry`, `StakeManager`, `RewardManager`, `Reputation`, `ContributionRegistry`, `DisputeResolution` and `Governance`.

The token and contract architecture remain provisional until physical and economic assumptions have been tested.

## Decisiones abiertas

Las siguientes decisiones siguen deliberadamente abiertas y no deben considerarse definidas todavía:

- **Lenguaje de implementación:** TBD
- **Licencia del proyecto:** TBD
- **Red de despliegue:** TBD
- **Modelo económico:** TBD

Estas decisiones se tomarán después de validar los requisitos técnicos, científicos y económicos del proyecto.

## Implementation language

**Not declared yet.**

The project intentionally does **not** prescribe a programming language at this stage. The implementation language or languages will be selected after the protocol, interfaces and system requirements are sufficiently specified.

This applies to:

- LEO node software
- signal processing and scientific computation
- P2P/network components
- explorer/frontend
- EVM smart contracts

The choice will be made from evidence and requirements rather than assumed in the architecture.

## Contributions and provenance

Code, algorithms, models, datasets, documentation, hardware designs, research and validation work should be traceable through contribution IDs, authorship, parent/fork relationships, Git hashes, citations, validation evidence and reward history.

Creating a fork alone should not generate a reward. Useful validated contribution should.

## LEO Explorer

A future explorer should show satellite/object tracks, observations, verification state, evidence, network nodes, historical data and anomalies.

Example:

`Observation #84721`

- Object: `UNKNOWN-034`
- Station
- Timestamp
- Frequency
- Doppler
- SNR
- Orbital consistency
- Independent observations
- Verifiers
- Stake
- Evidence
- Current state

## Node architecture

`Antenna/Dish → LNB/RF Front-End → SDR → Signal Processing → Observation Engine → Self-Verifier → P2P/Protocol Layer`

This is a functional architecture, not a language or implementation commitment.

## Multi-station observation

Future research may support cross-correlation, TDOA, FDOA, multilateration, improved orbit estimation and independent signal confirmation.

These are research targets, not current guarantees.

## Reproducible science

Important claims should be traceable through:

`raw evidence → processing → observation → verification → interpretation`

Preserve provenance, timestamps, processing/model versions, configuration, uncertainty, verification history and hashes.

## Security and safety

LEO Network is designed for **passive observation**. The project does not require jamming, spoofing, unauthorized satellite control or interference.

## Development phases

1. Architecture and protocol
2. Passive physical prototype
3. Verification and historical correlation
4. Distributed node network
5. LEO Explorer
6. Economic measurements and simulations
7. EVM/blockchain implementation

**No production token should be launched before the physical, verification and economic assumptions have been experimentally tested.**

## Repository structure

```text
LEO-Network/
├── README.md
├── .gitignore
├── docs/
│   ├── ARCHITECTURE.md
│   ├── PROTOCOL.md
│   ├── ECONOMICS.md
│   └── ROADMAP.md
├── leo-node/
├── leo-explorer/
├── contracts/
├── protocols/
├── research/
├── datasets/
└── simulations/
```

## Guiding principle

> **The network does not ask you to trust the observation. It gives you the evidence to verify it.**

**Observe. Verify. Prove. Contribute.**
