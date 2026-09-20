# LEO Network Architecture

## Layers

1. Physical: antenna/RF front-end, SDR, GNSS timing and host.
2. Observation: acquisition, DSP, Doppler and evidence extraction.
3. Verification: self-verification, orbital consistency, history and independent stations.
4. Network: node identity, P2P communication and evidence exchange.
5. Economic: stake, rewards, reputation and disputes.
6. Blockchain: registries, attestations, staking, rewards and governance.
7. Explorer: observations, tracks, verification and evidence.

## Node principle

Every node is both observer and verifier.

Initial conceptual workload: approximately 75% observation/self-verification and 25% third-party verification. This ratio is provisional.

## Evidence principle

Large scientific payloads remain off-chain. Hashes, provenance and attestations can be anchored on-chain.

## Epistemic principle

`UNKNOWN` is a first-class state. The architecture must preserve uncertainty rather than force identification.
