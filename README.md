# LEO Network

**Red distribuida de observación, verificación y datos científicos**

> Observar. Verificar. Probar. Contribuir.

LEO Network es una arquitectura experimental abierta para una red distribuida de nodos físicos capaces de recopilar, verificar, correlacionar y publicar evidencias sobre objetos en órbita terrestre baja (LEO) y, potencialmente, sobre otros fenómenos científicos.

## Estado

**Concepto / diseño experimental — no preparado para producción.**

La arquitectura, el protocolo, el modelo económico y el diseño del token están deliberadamente incompletos. Las mediciones con hardware real y las simulaciones deben preceder a las decisiones de producción.

## Principios fundamentales

- Ningún observador único.
- Ningún validador único.
- Ninguna base de datos única como única fuente de verdad.
- Evidencia antes que conclusiones.
- `UNKNOWN` es un resultado válido.
- Correlación no implica causalidad.
- Un error del sensor no es automáticamente fraude.
- Los datos históricos forman parte de la verificación.
- Los datos científicos pesados permanecen fuera de la cadena; los hashes y las atestaciones pueden anclarse en cadena.
- Observación pasiva por diseño: medición y análisis, no interferencia ni control.

## El nodo LEO

**LEO Node = Observar + Verificar + Apostar + Ganar**

Cada nodo puede observar señales físicas, realizar autoverificaciones locales, verificar observaciones de otros nodos, mantener la procedencia criptográfica, aportar stake como garantía económica y recibir recompensas por trabajo útil y verificable de forma independiente.

El objetivo conceptual actual de carga de trabajo es aproximadamente **75 % observación/autoverificación y 25 % verificación de terceros**. El protocolo final deberá hacer este parámetro configurable.

## Observación

Una observación puede contener marca temporal, identidad de la estación, posición geográfica, frecuencia, ancho de banda, potencia recibida, SNR, desplazamiento Doppler, tasa de cambio Doppler, azimut/elevación, características espectrales, características de huella RF, configuración del receptor, contexto orbital y hash de evidencia.

Los IQ en bruto, FFT, espectrogramas y demás evidencias de gran tamaño deberían permanecer normalmente fuera de la cadena.

## Verificación

La verificación puede combinar comprobaciones de calidad de señal, sincronización temporal, modelos orbitales como TLE/SGP4, comportamiento Doppler esperado, observaciones históricas, huellas RF, estaciones independientes cercanas y lejanas, y correlación temporal/espectral.

La independencia es una propiedad del protocolo. Diez máquinas controladas por un mismo operador no deberían contar automáticamente como diez testigos independientes.

## Estados epistémicos

Los estados posibles incluyen:

- `UNKNOWN`
- `OBSERVED`
- `SELF_VERIFIED`
- `CORRELATED`
- `VERIFIED`
- `DISPUTED`
- `INCONSISTENT`
- `ERROR`
- `FRAUD_DEMONSTRATED`

Una observación nunca debe verse obligada a adoptar la identidad de un satélite simplemente porque un modelo orbital sugiera una coincidencia.

## Proof of Useful Observation

El concepto económico es **Proof of Useful Observation (PoUO)**. Los nodos no deberían ganar simplemente por producir grandes cantidades de datos; las recompensas deberían depender de la utilidad y verificabilidad de la contribución.

Función conceptual de recompensa:

`REWARD = quality × utility × novelty × independence × coverage × verifiability`

Esto es una hipótesis de diseño, no una fórmula definitiva.

## Stake y veracidad

El stake actúa como garantía asociada a afirmaciones o trabajos de validación. Un trabajo correcto y verificado independientemente puede obtener recompensas; los errores normales del sensor o del algoritmo no deberían considerarse automáticamente fraude; un fraude demostrado conforme a las reglas del protocolo podría dar lugar a penalizaciones.

## Red de datos científicos

La arquitectura puede extenderse más allá de la observación LEO hacia datos atmosféricos, meteorológicos, incendios, superficie terrestre, actividad solar/geomagnética y otros conjuntos de datos científicos disponibles públicamente.

La red debería proporcionar procedencia, incertidumbre, reproducibilidad y herramientas de correlación.

**CORRELACIÓN ≠ CAUSALIDAD.**

## Blockchain

La dirección actual es una arquitectura **compatible con EVM**, con **Polygon** como ecosistema candidato.

Entre los contratos candidatos se incluyen `LEOToken`, `NodeRegistry`, `ObservationRegistry`, `VerificationRegistry`, `SatelliteRegistry`, `EvidenceRegistry`, `StakeManager`, `RewardManager`, `Reputation`, `ContributionRegistry`, `DisputeResolution` y `Governance`.

El token y la arquitectura de contratos siguen siendo provisionales hasta que se hayan probado las hipótesis físicas y económicas.

## Decisiones abiertas

Las siguientes decisiones siguen deliberadamente abiertas y no deben considerarse definidas todavía:

- **Lenguaje de implementación:** TBD
- **Licencia del proyecto:** TBD
- **Red de despliegue:** TBD
- **Modelo económico:** TBD

Estas decisiones se tomarán después de validar los requisitos técnicos, científicos y económicos del proyecto.

## Lenguaje de implementación

**Todavía no declarado.**

El proyecto no prescribe deliberadamente ningún lenguaje de programación en esta fase. El lenguaje o lenguajes de implementación se seleccionarán después de especificar suficientemente el protocolo, las interfaces y los requisitos del sistema.

Esto afecta a:

- Software del nodo LEO
- Procesamiento de señales y cálculo científico
- Componentes P2P/de red
- Explorer/frontend
- Smart contracts EVM

La elección se realizará a partir de requisitos y evidencia, no de una tecnología asumida de antemano.

## Contribuciones y procedencia

El código, los algoritmos, los modelos, los conjuntos de datos, la documentación, los diseños de hardware, la investigación y los trabajos de validación deberían poder rastrearse mediante identificadores de contribución, autoría, relaciones padre/fork, hashes de Git, citas, evidencias de validación e historial de recompensas.

Crear un fork por sí solo no debería generar una recompensa. La recompensa debería corresponder a una contribución útil y validada.

## LEO Explorer

Un futuro Explorer debería mostrar trayectorias de satélites/objetos, observaciones, estado de verificación, evidencias, nodos de la red, datos históricos y anomalías.

Ejemplo:

`Observation #84721`

- Objeto: `UNKNOWN-034`
- Estación
- Marca temporal
- Frecuencia
- Doppler
- SNR
- Consistencia orbital
- Observaciones independientes
- Verificadores
- Stake
- Evidencia
- Estado actual

## Arquitectura del nodo

`Antena/Parabólica → LNB/Front-End RF → SDR → Procesamiento de señal → Motor de observación → Autoverificador → Capa P2P/Protocolo`

Esta es una arquitectura funcional, no una decisión sobre lenguaje o implementación.

## Observación multiestación

Las investigaciones futuras pueden incluir correlación cruzada, TDOA, FDOA, multilateración, mejora de la estimación orbital y confirmación independiente de señales.

Son objetivos de investigación, no garantías actuales.

## Ciencia reproducible

Las afirmaciones importantes deberían poder rastrearse mediante:

`evidencia bruta → procesamiento → observación → verificación → interpretación`

Debe preservarse la procedencia, las marcas temporales, las versiones de procesamiento/modelo, la configuración, la incertidumbre, el historial de verificación y los hashes.

## Seguridad y uso responsable

LEO Network está diseñado para la **observación pasiva**. El proyecto no requiere jamming, spoofing, control no autorizado de satélites ni interferencias.

## Fases de desarrollo

1. Arquitectura y protocolo
2. Prototipo físico pasivo
3. Verificación y correlación histórica
4. Red distribuida de nodos
5. LEO Explorer
6. Mediciones y simulaciones económicas
7. Implementación EVM/blockchain

**No debería lanzarse ningún token de producción antes de probar experimentalmente las hipótesis físicas, de verificación y económicas.**

## Estructura del repositorio

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

## Principio rector

> **La red no te pide que confíes en la observación. Te proporciona la evidencia para verificarla.**

**Observar. Verificar. Probar. Contribuir.**
