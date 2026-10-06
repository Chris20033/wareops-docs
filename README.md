# WareOps — Documentación

> Base de conocimiento, especificación funcional, arquitectura y hoja de ruta técnica de **WareOps**: plataforma SaaS multiempresa para la gestión y control de inventarios distribuidos en múltiples sucursales y almacenes.

---

## 📖 Acerca del Proyecto

WareOps es un sistema diseñado como proyecto de portafolio de nivel profesional enfocado en resolver problemas reales de negocio e ingeniería de software:
- **Aislamiento multiempresa (Multi-tenancy):** Particionamiento lógico de datos con seguridad transversal por organización.
- **Consistencia transaccional de inventario:** Libro mayor (*inventory ledger*), movimientos auditables y prevención de sobreventas o existencias negativas.
- **Gestión operacional:** Catálogo unificado de productos, proveedores, sucursales, almacenes, órdenes de compra/venta y transferencias entre almacenes.
- **Idempotencia y auditoría:** Registro exhaustivo de operaciones críticas y tolerancia ante reintentos de red.

---

## 🗂️ Estructura de la Documentación

La documentación está organizada como un vault de [Obsidian](https://obsidian.md), estructurado en las siguientes secciones:

| Directorio | Contenido |
| --- | --- |
| [`00 Inicio/`](./00%20Inicio/) | Glosario de términos, supuestos de diseño e [Índice principal](./00%20Inicio/WareOps%20-%20%C3%8Dndice.md). |
| [`01 Producto/`](./01%20Producto/) | Visión del producto, alcance del MVP, módulos clave y roles de usuario. |
| [`02 Requisitos/`](./02%20Requisitos/) | Requisitos funcionales (RF), no funcionales (RNF), casos de uso y criterios de aceptación. |
| [`03 Dominio/`](./03%20Dominio/) | Entidades de dominio, modelo conceptual y reglas de negocio. |
| [`04 Base de Datos/`](./04%20Base%20de%20Datos/) | Diseño lógico, normalización a 3FN, diccionario de datos y catálogo de consultas Prisma. |
| [`05 Arquitectura/`](./05%20Arquitectura/) | Arquitectura global del sistema (monolito modular), backend (NestJS), frontend (Next.js), seguridad y despliegue. |
| [`06 Roadmap/`](./06%20Roadmap/) | Estado del MVP, plan de desarrollo y especificación detallada de sprints (`06 Roadmap/Sprints/`). |
| [`07 Diagramas/`](./07%20Diagramas/) | Diagramas de arquitectura en Mermaid, modelos entidad-relación (ER) y flujos críticos. |
| [`08 API/`](./08%20API/) | Convenciones REST, catálogo de endpoints, contratos y manejo estándar de errores HTTP. |
| [`09 ADR/`](./09%20ADR/) | Registro de decisiones de arquitectura (*Architecture Decision Records*). |

---

## 🗺️ Roadmap y Sprints

El desarrollo de WareOps sigue una metodología guiada por objetivos funcionales medibles descritos en [`06 Roadmap/Plan de Sprints.md`](./06%20Roadmap/Plan%20de%20Sprints.md). Cada sprint cuenta con su lista de verificación de entregables, pruebas y criterios de cierre en la carpeta [`06 Roadmap/Sprints/`](./06%20Roadmap/Sprints/):

- **Sprint 00:** Fundación (entorno, CI, PostgreSQL, health checks y tooling).
- **Sprint 01:** Identidad y Multi-tenancy (autenticación segura, organizaciones y RBAC).
- **Sprint 02:** Ubicaciones y Catálogo (sucursales, almacenes, productos y proveedores).
- **Sprint 03:** Núcleo de Inventario (saldos, movimientos, entradas y salidas consistentes).
- **Sprint 04:** Transferencias (movimientos entre almacenes atómicos e idempotentes).
- **Sprint 05:** Órdenes y Reservas (ciclo de orden, reservas de stock y liberación).
- **Sprint 06:** Supervisión (métricas, alertas de stock mínimo y auditoría).
- **Sprint 07:** Cierre de Portafolio (despliegue en producción, pruebas E2E y demo).

---

## 💻 Repositorios del Ecosistema WareOps

| Repositorio | Descripción |
| --- | --- |
| **`wareops-docs`** | Documentación funcional, técnica y arquitectura (este repositorio). |
| **`wareops-api`** | Backend NestJS, lógica de dominio, persistencia Prisma y API REST. |
| **`wareops-web`** | Frontend Next.js (App Router), interfaz de usuario y flujos operativos. |

---

## 🔍 Cómo Visualizar la Documentación

1. **GitHub:** Puedes navegar directamente por las carpetas y enlaces markdown desde el explorador web de este repositorio.
2. **Obsidian (Recomendado):**
   - Clona este repositorio:
     ```bash
     git clone https://github.com/Chris20033/wareops-docs.git
     ```
   - Abre Obsidian y selecciona **Open folder as vault** apuntando a la carpeta clonada.
   - Disfruta de la navegación con enlaces internos tipo wiki `[[...]]`, grafos de relaciones y visualización interactiva.
