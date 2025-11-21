# 📄 Resumen Ejecutivo del Proyecto Arquitectónico

## 🏢 Nombre del Cliente
_Zajana S.A.S._

## 🎯 Objetivo General del Proyecto
El objetivo del proyecto fue analizar, modelar y estructurar la arquitectura empresarial de Zajana S.A.S. alrededor de su producto principal Macia, una plataforma que integra múltiples fuentes de información para generar scores analíticos usados por entidades financieras y del sector real.

El análisis buscó identificar riesgos, dependencias, brechas normativas y oportunidades de mejora, con el fin de proponer una arquitectura futura más escalable, segura y alineada con las metas estratégicas de la organización, incluyendo una ruta de migración transitoria hacia Snowflake.

La arquitectura AS-IS evidenció una fuerte dependencia de servicios distribuidos en Azure, incluyendo SQL Database, Cosmos DB, Synapse, ML Studio, APIM y un acceso a fuentes externas mediado únicamente por VPN Gateway. Esta dispersión tecnológica generaba duplicidad de almacenamiento, fragmentación de procesos analíticos, falta de clasificación unificada en Purview, riesgos de exposición indirecta y costos operativos elevados. El diagnóstico permitió reconocer la necesidad de consolidar la analítica y gobernanza en una plataforma unificada como Snowflake.

## 🧱 Vistas Arquitectónicas Cubiertas

La siguiente tabla resume cada vista, sus principales diagramas y la relación que guarda con las demás:

| Vista                | Resumen breve                                                                                                        | Diagramas principales                                         | Relación con otras vistas                                                                                                    |
|----------------------|----------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------|
| Negocio              | Describe los procesos clave de Zajana y cómo se gestiona el ciclo de vida del producto Macia y la migración a Snowflake. | BPMN de procesos clave, BPMN de migración                     | Define qué actividades requieren datos (*información*), qué funciones deben soportar las *aplicaciones* y qué capacidades debe habilitar la *infraestructura*. |
| Información          | Modela las entidades de datos, sus atributos y relaciones que soportan el cálculo de *scores* y la operación de Macia. | Modelo Entidad–Relación (ERD)                                 | Provee los objetos de información que consumen los procesos de negocio, las APIs de *aplicaciones* y los servicios de *infraestructura y seguridad*.          |
| Aplicaciones         | Muestra los sistemas y contenedores que implementan la lógica de negocio y exponen servicios a clientes y operadores. | C1 (Contexto), C2 (Contenedores actual), C2 mejora (Snowflake) | Conecta procesos de *negocio* con datos específicos (*información*) y se apoya en la *infraestructura* para desplegar portales, APIs y servicios analíticos.   |
| Infraestructura      | Detalla los servicios de Azure y su posterior evolución hacia Snowflake, incluyendo redes, cómputo, almacenamiento y analítica. | Diagramas de infraestructura actual y mejorada                | Es la base técnica sobre la que se despliegan las *aplicaciones*, aloja los repositorios de *información* y sirve de ancla para los controles de *seguridad*.   |
| Seguridad            | Recoge los controles de identidad, protección de datos, monitoreo y cumplimiento normativo aplicados a toda la solución. | Tabla STRIDE, checklist normativo    | Protege al resto de vistas garantizando que *negocio*, *información*, *aplicaciones* e *infraestructura* cumplan requisitos de confidencialidad, integridad y trazabilidad. |

## 🧩 Hallazgos Clave

- ❗ Dependencia crítica en un único desarrollador senior, que retrasó la migración y elevó riesgo operativo.
- 🔄 Políticas de clasificación y retención entre Azure y Snowflake no alineadas, afectando cumplimiento normativo (Ley 1581, Ley 1266).
- 🗂️ Duplicidad de almacenamiento entre SQL, Cosmos, Synapse y Delta Lake, generando costos y complejidad operativa.
- 🌐 Dependencia fuerte de fuentes externas y CRM Dynamics 365, con riesgos de disponibilidad, latencia y amenazas STRIDE (spoofing, tampering, EoP).
- 🔐 Seguridad robusta en Azure, pero sin equivalente en Snowflake (auditoría, cifrado, trazabilidad, gobernanza).
- 🛡️ Ingesta protegida solo por VPN Gateway, sin firewall dedicado ni VNET específica para la capa de buro.
- 📌 Brechas en la integración con el CRM y fuentes externas impedían trazabilidad completa del ciclo de consulta y facturación.
- 📌 Brechas de integración entre sistemas internos, fuentes externas y CRM impedían trazabilidad completa de ciclo de consulta y facturación.

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
