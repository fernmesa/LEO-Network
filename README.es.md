# LEO Network

**Red distribuida de observación, verificación y datos científicos**

> Observar. Verificar. Probar. Contribuir.

Este documento es la versión en español del [README principal](README.md).

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

## Observación y verificación

Una observación puede contener marca temporal, identidad de la estación, posición geográfica, frecuencia, ancho de banda, potencia recibida, SNR, desplazamiento Doppler, tasa de cambio Doppler, azimut/elevación, características espectrales, huella RF, configuración del receptor, contexto orbital y hash de evidencia.

La verificación puede combinar calidad de señal, sincronización temporal, modelos orbitales como TLE/SGP4, comportamiento Doppler esperado, observaciones históricas, huellas RF, estaciones independientes cercanas y lejanas y correlación temporal/espectral.

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

Función conceptual:

`REWARD = quality × utility × novelty × independence × coverage × verifiability`

Es una hipótesis de diseño, no una fórmula definitiva.

## Stake y veracidad

El stake actúa como garantía asociada a afirmaciones o trabajos de validación. Un trabajo correcto y verificado independientemente puede obtener recompensas; los errores normales del sensor o del algoritmo no deberían considerarse automáticamente fraude; un fraude demostrado conforme a las reglas del protocolo podría dar lugar a penalizaciones.

## Red de datos científicos

La arquitectura puede extenderse a datos atmosféricos, meteorológicos, incendios, superficie terrestre, actividad solar/geomagnética y otros conjuntos de datos científicos disponibles públicamente.

La red debería proporcionar procedencia, incertidumbre, reproducibilidad y herramientas de correlación.

**CORRELACIÓN ≠ CAUSALIDAD.**

## Blockchain

La dirección actual es una arquitectura **compatible con EVM**, con **Polygon** como ecosistema candidato.

El token y la arquitectura de contratos siguen siendo provisionales hasta que se hayan probado las hipótesis físicas y económicas.

## Decisiones abiertas

Las siguientes decisiones siguen deliberadamente abiertas:

- **Lenguaje de implementación:** TBD
- **Licencia del proyecto:** TBD
- **Red de despliegue:** TBD
- **Modelo económico:** TBD

Estas decisiones se tomarán después de validar los requisitos técnicos, científicos y económicos del proyecto.

## Explorer

Un futuro Explorer debería mostrar trayectorias de satélites/objetos, observaciones, estado de verificación, evidencias, nodos de la red, datos históricos y anomalías.

## Ciencia reproducible

Las afirmaciones importantes deberían poder rastrearse mediante:

`evidencia bruta → procesamiento → observación → verificación → interpretación`

Debe preservarse la procedencia, las marcas temporales, las versiones de procesamiento/modelo, la configuración, la incertidumbre, el historial de verificación y los hashes.

## Seguridad y uso responsable

LEO Network está diseñado para la **observación pasiva**. El proyecto no requiere jamming, spoofing, control no autorizado de satélites ni interferencias.

## Principio rector

> **La red no te pide que confíes en la observación. Te proporciona la evidencia para verificarla.**

**Observar. Verificar. Probar. Contribuir.**
