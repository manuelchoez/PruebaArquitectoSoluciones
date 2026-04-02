# Diseño de Arquitectura – Sistema de Banca por Internet BP

**Autor:** Teófilo Manuel Chóez Arteaga  
**Fecha:** 01 de abril del 2026  
**GitHub:** 

---

## Índice
1. [Introducción](#introducción)
2. [Objetivos](#objetivos)
   - [Objetivo General](#objetivo-general)
   - [Objetivos Específicos](#objetivos-específicos)
3. [Definición del Problema y Alcance](#definición-del-problema-y-alcance)
   - [Problema](#problema)
   - [Alcance](#alcance)
4. [Análisis de Decisiones Arquitectónicas](#análisis-de-decisiones-arquitectónicas)
5. [Diseño de la Solución](#diseño-de-la-solución)
   - [Nivel 1: Diagrama de Contexto](#nivel-1-diagrama-de-contexto)
   - [Nivel 2: Diagrama de Contenedores](#nivel-2-diagrama-de-contenedores)
   - [Nivel 3: Diagrama de Componentes](#nivel-3-diagrama-de-componentes)
6. [Arquitectura de Seguridad y Autenticación](#arquitectura-de-seguridad-y-autenticación)
7. [Infraestructura y Excelencia Operativa](#infraestructura-y-excelencia-operativa)
8. [Cumplimiento Normativo](#cumplimiento-normativo)
9. [Conclusiones](#conclusiones)

---

## 1. Introducción

Este repositorio contiene la documentación y diagramas del diseño arquitectónico para el nuevo sistema de Banca por Internet de la entidad financiera BP. El objetivo es ofrecer una plataforma moderna, segura y altamente disponible, priorizando el uso de servicios en la nube (Azure) y prácticas de arquitectura orientadas a microservicios, observabilidad y cumplimiento normativo.

La estructura del repositorio es la siguiente:
- **src/docs/**: Documentación detallada del análisis, decisiones y justificaciones técnicas.
- **src/diagrams/**: Diagramas C4 (contexto, contenedores, componentes) y otros artefactos visuales de arquitectura.

## 2. Objetivos

### Objetivo General
Diseñar la arquitectura del sistema de Banca por Internet para BP utilizando el modelo C4, garantizando un ecosistema escalable, disponible y seguro en Microsoft Azure.

### Objetivos Específicos
- Diseñar aplicaciones Frontend (SPA y Móvil) integradas mediante el patrón BFF (Backend for Frontend).
- Implementar un sistema de Onboarding con validación de biometría facial.
- Asegurar la plataforma utilizando OAuth 2.0.
- Integrar sistemas de notificaciones con múltiples proveedores (Mailgun, Eclisoft, ENExT, ALtScore).
- Garantizar excelencia operativa y auto-healing con observabilidad (Prometheus, Grafana, Jaeger, Sentry).
- Gestionar eficientemente los costos en Azure.

## 3. Definición del Problema y Alcance

### Problema
BP requiere modernizar sus canales digitales para que los clientes interactúen con el Core bancario y un sistema independiente de detalles de clientes. La normativa exige auditoría estricta y notificación obligatoria de movimientos financieros por al menos dos canales.

### Alcance
El diseño abarca una SPA y una app móvil multiplataforma, integración en Azure (API Management), microservicios core (Onboarding, Transacciones, Clientes, Notificaciones), bases de datos de auditoría y caché (Redis), infraestructura cloud, observabilidad, seguridad y estimación de costos.

## 4. Análisis de Decisiones Arquitectónicas

- **Azure** como nube principal por cumplimiento normativo y servicios administrados.
- **Patrón BFF** para optimizar la experiencia de usuario y encapsular lógica compleja.
- **Redis** para mejorar tiempos de respuesta y reducir carga sobre el Core.
- **Notificaciones** con múltiples proveedores para cumplir normativas y asegurar entrega.
- **Sentry** para monitoreo de errores en tiempo real.

## 5. Diseño de la Solución

### Nivel 1: Diagrama de Contexto
El sistema orquesta consultas y transacciones, validando identidades y notificando movimientos a través de sistemas de correo/SMS.

### Nivel 2: Diagrama de Contenedores
- App Móvil y Web acceden vía Azure API Management.
- Microservicios: Onboarding (biometría), Transacciones, Clientes (con Redis), Notificaciones.
- Auditoría de movimientos en base de datos dedicada.

### Nivel 3: Diagrama de Componentes
Ejemplo: Microservicio de Transacciones y Movimientos
- Transaction Controller → Movement Service / Transfer Coordinator
- Core API Adapter (SOAP/XML)
- Audit Publisher (eventos asíncronos a auditoría)

## 6. Arquitectura de Seguridad y Autenticación

- OAuth 2.0 con Authorization Code + PKCE para apps móviles y SPA.
- Onboarding con biometría facial orquestada desde el BFF.
- Acceso posterior mediante huella digital o usuario/clave.

## 7. Infraestructura y Excelencia Operativa

- Alta disponibilidad (HA) y recuperación ante desastres (DR) en Azure.
- Observabilidad: Prometheus (métricas), Grafana (dashboards), Jaeger (tracing), Sentry (errores).
- Políticas de auto-escalado y control de costos.
- Redis y API Management para optimización y protección ante DDoS.

## 8. Cumplimiento Normativo

- Registro inmutable de acciones en base de datos de auditoría.
- Notificaciones redundantes (Mailgun/Eclisoft).
- Cumplimiento de Ley de Datos Personales y PCI-DSS (si aplica).

## 9. Conclusiones

El diseño propuesto responde a los requerimientos de BP, garantizando robustez, seguridad, baja latencia y cumplimiento normativo. La adopción de Azure, patrones modernos y un stack de observabilidad aseguran excelencia operativa y tolerancia a fallos.

---

> Para más detalles, consulte la documentación en `src/docs/` y los diagramas en `src/diagrams/`.
