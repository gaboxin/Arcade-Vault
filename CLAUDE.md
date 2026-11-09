# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Proyecto

Arcade Vault: plataforma para jugar online y competir por la mayor cantidad de puntos. El README indica que usa Spec Driven Design (`/spec` y `/spec-impl`), con las skills de `Klerith/fernando-skills` (`npx skills@latest add Klerith/fernando-skills`).

Estado actual: el código en `app/` es todavía el scaffold de Create Next App (`layout.tsx` con metadata por defecto, `page.tsx` inicial). La UI objetivo aún no está portada.


## Stack y advertencias

- Next.js 16.4.5, React 19.3, TypeScript, Tailwind CSS v4 (vía `@tailwindcss/turbopack`, configurado en `next.config.ts` como regla de Turbopack para `*.css`; el CSS se importa con `@import "tailwindcss"` en `app/globals.css`).
- **Esta versión de Next.js tiene cambios incompatibles** respecto a lo conocido (ver `AGENTS.md`): antes de escribir código, leer la guía relevante en `node_modules/next/dist/docs/` (`01-app`, `02-pages`, etc.).
- `next.config.ts` activa `cacheComponents`, `partialPrefetching` y `experimental.agentFeedback`; esto afecta cómo se hace data fetching/caching en App Router.
- Los tipos globales como `LayoutProps<"/">` se usan en `app/layout.tsx` (props tipadas por ruta).
- Alias de imports: `@/*` apunta a la raíz del repo.
## Skills
- Usa siempre /frontend-desingn para hacer interfaces de usuario
## Referencia de diseño (`resources/`)

`resources/templates/` contiene un prototipo HTML/React-vía-CDN (sin build) que sirve como diseño a portar a Next.js; `resources.zip` es el mismo material comprimido. Archivos: `Arcade Vault.html` (entrada), `app.jsx` (estado raíz y ruteo), `nav.jsx`, `auth.jsx`, `biblioteca.jsx`, `detalle.jsx`, `reproductor.jsx`, `salon.jsx`, `data.jsx` (datos), `styles.css`.

Comportamiento del prototipo que el port debe considerar:
- Ruteo por estado serializado en `location.hash` (`{ name: "biblioteca" | ... }`); vistas: biblioteca, detalle, reproductor, salón (ranking), auth.
- Persistencia solo en `localStorage`: sesión en `av_user`, puntajes en `av_scores` (lista de entradas con `at: Date.now()`).
- Los componentes comparten un único scope global (los hooks se renombran, p. ej. `useStateApp`, para evitar colisiones); al portar a módulos ES esto desaparece.
