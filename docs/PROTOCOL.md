# LEO Network Protocol

## Observation lifecycle

`CAPTURE → OBSERVE → SELF_VERIFY → PUBLISH → INDEPENDENT_VERIFY → STATE`

Possible states:

- `UNKNOWN`
- `OBSERVED`
- `SELF_VERIFIED`
- `CORRELATED`
- `VERIFIED`
- `DISPUTED`
- `INCONSISTENT`
- `ERROR`
- `FRAUD_DEMONSTRATED`

## Verification

Verification should combine independent evidence sources.

Independence considers operator, hardware, geography, time, software lineage and historical dependence.

## Error versus fraud

A failed measurement is not automatically fraudulent. Penalties require explicit protocol conditions and evidence of deliberate or protocol-defined malicious behaviour.

## Historical correlation

Historical observations are active verification evidence.
