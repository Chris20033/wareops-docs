# Frontend

## Estructura esperada

```text
src/
├── app/
│   ├── (auth)/
│   └── (dashboard)/
├── features/
├── components/
├── lib/
│   ├── api/
│   ├── auth/
│   └── validation/
├── stores/
└── test/
```

`app` compone rutas y layouts; `features` contiene comportamiento por módulo; `components` contiene UI reutilizable sin reglas de negocio; `lib` alberga infraestructura; `stores` conserva sólo estado cliente.

## Estado y datos

- TanStack Query administra datos remotos, caché, reintentos e invalidaciones.
- Zustand conserva organización activa y preferencias de interfaz; no duplica entidades del servidor.
- Filtros, página y orden se reflejan en search params para permitir enlaces y navegación reproducible.
- El access token vive en memoria. Al recargar, la web intenta renovar mediante cookie antes de mostrar contenido protegido.

## Formularios y contrato

- React Hook Form con esquemas Zod cercanos a cada feature.
- Cliente HTTP central añade bearer token, `X-Organization-Id` y `X-Request-Id`.
- Un único intento de refresh coordina solicitudes que reciben `401`; si falla, limpia sesión y dirige a login.
- Errores de campo y generales se traducen desde el contrato de errores sin exponer detalles internos.

## Interfaz

- Tailwind y shadcn/ui con tokens de diseño compartidos.
- Navegación visible según capacidades, sin tratarla como control de seguridad.
- Tablas responsivas para escritorio/tablet y vistas compactas para operaciones críticas en móvil.
- Formularios con etiquetas, foco visible, mensajes asociados y navegación por teclado.

## Pruebas

Vitest y React Testing Library cubren formularios, estados y permisos visuales. Playwright verifica el recorrido desplegado de login, entrada, transferencia, orden y auditoría.

## Fundación ejecutable

- La web usa Node.js 24.x LTS, npm 11.x y un `package-lock.json` consumido con `npm ci`.
- `NEXT_PUBLIC_API_BASE_URL` contiene la URL pública de la API, incluida la base `/api/v1`; en desarrollo usa `http://localhost:3001/api/v1`.
- El layout raíz instala el `QueryClientProvider`. Zustand queda disponible para estado cliente, pero los stores de sesión y organización se implementan en Sprint 02.
- Mientras no existan flujos de negocio, `/` muestra únicamente el estado técnico, responsivo y accesible de la fundación frontend.
- Los comandos locales de referencia son `npm run format:check`, `npm run lint`, `npm run test:run` y `npm run build`.
