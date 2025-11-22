# 📄 Resumen Ejecutivo del Proyecto Arquitectónico

## 🏢 Nombre del Cliente
_Zajana S.A.S._

## 🎯 Objetivo General del Proyecto
El objetivo del proyecto fue analizar, modelar y estructurar la arquitectura empresarial de Zajana S.A.S. alrededor de su producto principal Macia, una plataforma que integra múltiples fuentes de información para generar scores analíticos usados por entidades financieras y del sector real.

El análisis buscó identificar riesgos, dependencias, brechas normativas y oportunidades de mejora, con el fin de proponer una arquitectura futura más escalable, segura y alineada con las metas estratégicas de la organización, incluyendo una ruta de migración transitoria hacia Snowflake.

La arquitectura AS-IS evidenció una fuerte dependencia de servicios distribuidos en Azure, incluyendo SQL Database, Cosmos DB, Synapse, ML Studio, APIM y un acceso a fuentes externas mediado únicamente por VPN Gateway. Esta dispersión tecnológica generaba duplicidad de almacenamiento, fragmentación de procesos analíticos, falta de clasificación unificada en Purview, riesgos de exposición indirecta y costos operativos elevados. El diagnóstico permitió reconocer la necesidad de consolidar la analítica y gobernanza en una plataforma unificada como Snowflake.

## 🧱 Vistas Arquitectónicas Cubiertas

La siguiente tabla resume cada vista, sus principales diagramas y la relación que guarda con las demás:

| **Vista** | **Alcance de la Solución** | **Resumen breve** | **Diagramas principales** | **Relación con otras vistas** |
|----------|-----------------------------|--------------------|---------------------------|-------------------------------|
| **Negocio** | BPMN de oportunidades, desarrollo, gestión de fuentes y migración (incluyendo suplente técnico). | Describe los procesos estratégicos y operativos de Zajana, incluyendo el ciclo de vida del producto *Macia*, la interacción con clientes/aliados y la migración hacia Snowflake. Identifica actores, reglas y puntos críticos. | BPMN de procesos clave; BPMN del proceso de migración. | Define qué datos requiere cada proceso (*información*), qué funcionalidades deben implementar los sistemas (*aplicaciones*) y qué capacidades tecnológicas son necesarias (*infraestructura*). |
| **Información / Datos** | ERD centralizado de clientes, transacciones, cartera, empleadores e indicadores analíticos. | Modela las entidades, atributos y relaciones que soportan scoring, trazabilidad, reglas de negocio, operaciones y analítica. Incluye linaje y calidad de datos. | Modelo Entidad–Relación (ERD). | Provee los objetos de información consumidos por los procesos (*negocio*), expuestos/gestionados por APIs (*aplicaciones*) y alojados en la *infraestructura*. Es base para los controles de privacidad y gobernanza (*seguridad* y *cumplimiento*). |
| **Aplicaciones / Sistemas** | C1 y C2 actual + C2 objetivo, integrando APIs, frontends, backend, CRM y Snowflake. | Muestra los sistemas, microservicios y módulos que implementan la lógica del negocio, exponen servicios a operadores/clientes y conectan con pipelines analíticos en Snowflake. | C1 (Contexto), C2 actual (Contenedores), C2 objetivo (Snowflake + CRM). | Implementa los procesos de *negocio* usando los datos de *información*. Se despliega sobre la *infraestructura* y aplica los controles de *seguridad*. |
| **Infraestructura** | Mapa de infraestructura Azure: VNETs, SQL, Cosmos DB, APIM, Synapse, monitoreo y arquitectura futura con Snowflake. | Describe la arquitectura técnica actual en Azure y su evolución: redes, cómputo, almacenamiento, analítica, orquestación y observabilidad. | Diagramas de infraestructura actual y objetivo (Azure → Snowflake). | Hospeda las *aplicaciones*, almacena y transporta los activos de *información* y habilita los mecanismos de *seguridad* y *cumplimiento*. |
| **Seguridad** | STRIDE, controles de Entra ID, APIM, WAF, Purview, Sentinel, cifrado, políticas de datos y gobernanza. | Define controles de identidad, protección de datos, monitoreo, cifrado, amenazas y mitigaciones aplicadas a toda la solución. | Tabla STRIDE; checklist de controles técnicos. | Cubre transversalmente todas las vistas: protege procesos (*negocio*), asegura datos (*información*), garantiza políticas en *aplicaciones* y se integra a la *infraestructura*. |
| **Cumplimiento Normativo** | Checklist legal según Ley 1581, Ley 1266, ISO 27001, gestión de retención, trazabilidad y clasificación de datos. | Integra los requisitos regulatorios que deben cumplir datos, procesos, sistemas y flujos entre Azure y Snowflake. | Checklist normativo y matriz de brechas. | Alinea *negocio*, *información*, *aplicaciones*, *infraestructura* y *seguridad* con el marco legal y buenas prácticas de protección de datos y TI. |

Esto se puede ver más a detalle en el siguiente link: 
[https://github.com/MariSalas23/AREM-Wiki/wiki/Integraci%C3%B3n-de-Vistas-%E2%80%90-Zajana-S.A.S.](https://github.com/MariSalas23/AREM-Wiki/wiki/Integraci%C3%B3n-de-Vistas-%E2%80%90-Zajana-S.A.S.)

## 🧩 Hallazgos Clave

- Dependencia crítica en un único desarrollador senior, que retrasó la migración y elevó riesgo operativo.
- Políticas de clasificación y retención entre Azure y Snowflake no alineadas, afectando cumplimiento normativo (Ley 1581, Ley 1266).
- Duplicidad de almacenamiento entre SQL, Cosmos, Synapse y Delta Lake, generando costos y complejidad operativa.
- Dependencia fuerte de fuentes externas y CRM Dynamics 365, con riesgos de disponibilidad, latencia y amenazas STRIDE (spoofing, tampering, EoP).
- Seguridad robusta en Azure, pero sin equivalente en Snowflake (auditoría, cifrado, trazabilidad, gobernanza).
- Ingesta protegida solo por VPN Gateway, sin firewall dedicado ni VNET específica para la capa de buro.
- Brechas en la integración con el CRM y fuentes externas impedían trazabilidad completa del ciclo de consulta y facturación.
- Brechas de integración entre sistemas internos, fuentes externas y CRM impedían trazabilidad completa de ciclo de consulta y facturación.

## 🚀 Recomendaciones Principales

- Implementar una migración transitoria con doble escritura, dominios de datos y switchover controlado.
- Sincronizar Microsoft Purview con Snowflake para clasificación, linaje, auditoría y políticas de retención.
- Configurar Time Travel y Fail-safe en Snowflake para garantizar retención alineada a las políticas actuales.
- Reducir sobrecostos analíticos mediante warehouse auto-suspend, optimización de cargas y monitoreo de consumo.
- Fortalecer controles de APIs con rate limiting, reglas WAF específicas y autenticación token-based integrada con Entra ID.
- Mantener suplente técnico para evitar puntos únicos de falla.
- Desplegar firewall corporativo y VNET dedicada para reducir exposición y fortalecer arquitectura Zero Trust.

## 💡 Reflexión Final

El trabajo con Zajana S.A.S. permitió aplicar de manera práctica los conceptos de arquitectura empresarial en un contexto real, integrando procesos, datos, aplicaciones, infraestructura y seguridad dentro de una visión unificada. El equipo fortaleció habilidades de análisis estructurado, modelado, análisis normativo, documentación con trazabilidad entre capas y comunicación ejecutiva de soluciones tecnológicas.

La propuesta final habilita una transición segura hacia Snowflake, mejora la gobernanza de datos y consolida una arquitectura alineada con la estrategia del negocio, cumpliendo las exigencias del entorno regulado en el que opera la organización.

---

_Este resumen ejecutivo forma parte de la entrega final del curso AREM - Arquitectura Empresarial - Universidad de La Sabana._
