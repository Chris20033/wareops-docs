# WareOps

> Documentación funcional y técnica de una plataforma multiempresa para gestionar inventario en múltiples sucursales y almacenes.

## Navegación

- [[00 Inicio/Glosario|Glosario]]
- [[00 Inicio/Decisiones y Supuestos|Decisiones y supuestos]]
- [[01 Producto/Visión del Producto|Visión del producto]]
- [[01 Producto/Alcance y MVP|Alcance y MVP]]
- [[01 Producto/Usuarios y Roles|Usuarios y roles]]
- [[01 Producto/Módulos Principales|Módulos principales]]
- [[02 Requisitos/Requisitos Funcionales|Requisitos funcionales]]
- [[02 Requisitos/Requisitos No Funcionales|Requisitos no funcionales]]
- [[02 Requisitos/Casos de Uso|Casos de uso]]
- [[02 Requisitos/Criterios de Aceptación|Criterios de aceptación]]
- [[02 Requisitos/Matriz de Trazabilidad|Matriz de trazabilidad]]
- [[03 Dominio/Entidades|Entidades del dominio]]
- [[03 Dominio/Reglas de Negocio|Reglas de negocio]]
- [[03 Dominio/Modelo Conceptual|Modelo conceptual]]
- [[04 Base de Datos/Diseño Lógico|Diseño lógico]]
- [[04 Base de Datos/Diccionario de Datos|Diccionario de datos]]
- [[04 Base de Datos/Normalización a Tercera Forma Normal|Normalización a 3FN]]
- [[04 Base de Datos/Catálogo de Consultas Prisma|Catálogo de consultas Prisma]]
- [[05 Arquitectura/Arquitectura del Sistema|Arquitectura del sistema]]
- [[05 Arquitectura/Frontend|Arquitectura frontend]]
- [[05 Arquitectura/Backend|Arquitectura backend]]
- [[05 Arquitectura/Autenticación y Seguridad|Autenticación y seguridad]]
- [[05 Arquitectura/Integraciones Externas|Integraciones externas]]
- [[05 Arquitectura/Despliegue|Despliegue]]
- [[06 Roadmap/MVP|Estado del MVP]]
- [[06 Roadmap/Roadmap de Desarrollo|Roadmap de desarrollo]]
- [[06 Roadmap/Plan de Sprints|Plan de sprints]]
- [[06 Roadmap/Funcionalidades Futuras|Funcionalidades futuras]]
- [[07 Diagramas/Arquitectura|Diagrama de arquitectura]]
- [[07 Diagramas/Modelo ER|Diagrama entidad-relación]]
- [[07 Diagramas/ER - Identidad y RBAC|ER de identidad y RBAC]]
- [[07 Diagramas/ER - Ubicaciones y Catálogo|ER de ubicaciones y catálogo]]
- [[07 Diagramas/ER - Inventario y Transferencias|ER de inventario y transferencias]]
- [[07 Diagramas/ER - Órdenes y Reservas|ER de órdenes y reservas]]
- [[07 Diagramas/ER - Idempotencia y Auditoría|ER de idempotencia y auditoría]]
- [[07 Diagramas/Flujos Críticos|Flujos críticos]]
- [[08 API/Convenciones de API|Convenciones de API]]
- [[08 API/Errores|Errores de API]]
- [[08 API/Catálogo de Endpoints|Catálogo de endpoints]]
- [[09 ADR/Índice de ADR|Registro de decisiones de arquitectura]]

## Repositorios

| Repositorio | Responsabilidad |
| --- | --- |
| `wareops-docs` | Documentación funcional, técnica y decisiones. |
| `wareops-api` | API NestJS, reglas de negocio y persistencia. |
| `wareops-web` | Aplicación Next.js consumida por los usuarios. |

## Estado actual

El proyecto se encuentra en fase de definición. La documentación describe el objetivo del MVP; la implementación todavía está pendiente. El estado ejecutable se mantiene en [[06 Roadmap/MVP]].

## Principio de alcance

WareOps es un proyecto de portafolio funcional. Debe demostrar aislamiento multiempresa, autorización, consistencia de inventario, auditoría y calidad automatizada sin incorporar complejidad operativa que no contribuya a esas capacidades.
