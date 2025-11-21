# 📄 Resumen Ejecutivo del Proyecto Arquitectónico

## 🏢 Nombre del Cliente
_Zajana S.A.S._

## 🎯 Objetivo General del Proyecto
El objetivo del proyecto fue analizar, modelar y estructurar la arquitectura empresarial de Zajana S.A.S. alrededor de su producto principal Macia, una plataforma que integra múltiples fuentes de información para generar scores analíticos usados por entidades financieras y del sector real.

El análisis buscó identificar riesgos, dependencias, brechas normativas y oportunidades de mejora, con el fin de proponer una arquitectura futura más escalable, segura y alineada con las metas estratégicas de la organización, incluyendo una ruta de migración transitoria hacia Snowflake.

## 🧱 Vistas Arquitectónicas Cubiertas

| Vista                  | Alcance de la Solución                      |
|------------------------|---------------------------------------------|
| Procesos de Negocio    | Modelado BPMN de procesos clave (oportunidades, desarrollo, gestión de fuentes) y BPMN de migración a Snowflake incluyendo suplente técnico. |
| Información / Datos    | Modelo ERD con entidades centrales (clientes, transacciones, cartera, empleadores, indicadores analíticos) y flujos de información.    |
| Aplicaciones / Sistemas| Diagramas C1 y C2 (actual y futuro), mostrando APIs, portales, backend, Snowflake y fuentes externas.                |
| Infraestructura        | Mapa de infraestructura Azure, VNETs, SQL, Cosmos, API Management, Synapse, observabilidad, y arquitectura objetivo con Snowflake. |
| Seguridad              | Análisis STRIDE, controles de Entra ID, MFA, APIM, WAF, Purview, Sentinel y revisión de amenazas. |
| Cumplimiento Normativo | Checklist legal alineado con Ley 1581, Ley 1266, ISO 27001, y hallazgos aplicables a la migración hacia Snowflake. |

## 🧩 Hallazgos Clave

- ❗ Dependencia crítica en un único perfil senior durante la migración a Snowflake, lo cual generó retrasos y riesgos operativos.
- 🔄 La clasificación y retención de datos en Snowflake aún no se encuentra alineada con Purview, lo que puede afectar el cumplimiento normativo.
- 📌 Existen oportunidades de mejora en [ejemplo: integración entre sistemas de pagos y CRM].El modelo actual presenta duplicidad de almacenamiento entre SQL, Cosmos y servicios analíticos, generando sobrecostos y fragmentación de datos.
- 💬 Las APIs expuestas dependen fuertemente de proveedores externos, elevando riesgos de disponibilidad y latencia.
- 🔐 Aunque existen controles de seguridad sólidos en Azure, Snowflake requiere extender trazabilidad, auditoría y retención para garantizar continuidad regulatoria.

## 🚀 Recomendaciones Principales

- Implementar la ruta de migración transitoria con fases: doble escritura, migración por dominios de datos, switchover controlado y eliminación final de servicios redundantes.
- Sincronizar Microsoft Purview con Snowflake, extendiendo clasificación automática, retención y monitoreo.
- Configurar Time Travel y Fail-safe en Snowflake para garantizar retención alineada a las políticas actuales.
- Reducir sobrecostos analíticos mediante warehouse auto-suspend, optimización de cargas y monitoreo de consumo.
- Fortalecer controles de APIs con rate limiting, reglas WAF específicas y autenticación token-based integrada con Entra ID.
- Continuar incorporando el suplente técnico como medida operativa para evitar puntos únicos de falla en procesos críticos.

## 💡 Reflexión Final

El trabajo con Zajana S.A.S. permitió aplicar de manera práctica los conceptos de arquitectura empresarial en un contexto real, integrando procesos, datos, aplicaciones, infraestructura y seguridad dentro de una visión unificada. El equipo fortaleció habilidades de análisis estructurado, modelado, análisis normativo, documentación con trazabilidad entre capas y comunicación ejecutiva de soluciones tecnológicas.

La propuesta final habilita una transición segura hacia Snowflake, mejora la gobernanza de datos y consolida una arquitectura alineada con la estrategia del negocio, cumpliendo las exigencias del entorno regulado en el que opera la organización.

---

_Este resumen ejecutivo forma parte de la entrega final del curso AREM - Arquitectura Empresarial - Universidad de La Sabana._
