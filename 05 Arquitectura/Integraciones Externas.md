# Integraciones Externas

## Estado del MVP

WareOps no depende de integraciones externas funcionales en el MVP. No se enviará correo, no habrá almacenamiento de archivos, pagos, ERP, comercio electrónico ni transportistas.

Las invitaciones generan un enlace copiable en la interfaz. PostgreSQL puede ser administrado y los destinos de despliegue pueden ser servicios externos, pero se consideran infraestructura intercambiable, no integraciones de dominio.

## Regla para incorporar una integración

Toda integración futura deberá documentar propósito, datos enviados y recibidos, autenticación, límites, timeout, reintentos, idempotencia, fallos, observabilidad, variables de entorno y estrategia de sustitución. Su incorporación requiere actualizar alcance y un ADR cuando cree acoplamiento arquitectónico.

Véase [[../06 Roadmap/Funcionalidades Futuras|Funcionalidades futuras]].
