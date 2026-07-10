# AGENTS.md

## Descripción del proyecto
Landing page de portfolio personal (no producción real). Proyecto de práctica orientado a desarrollar habilidades de desarrollo asistido por IA, con foco en diseño visual sólido inspirado en una referencia dada, y SEO técnico correcto.

## Stack técnico
- **Framework:** Astro (renderizado estático por defecto — ideal para contenido mayormente estático como una landing)
- **Componentes interactivos:** React + TypeScript como "islands" de Astro, usados SOLO donde haya interactividad real (ej: menú mobile, acordeón, validación de formulario). Todo lo demás va en `.astro` puro.
- **Estilos:**
  - Componentes `.astro` → `<style>` scoped nativo de Astro (el scoping es automático, no hay que inventar convención de nombres para evitar colisiones)
  - Componentes `.tsx` → CSS Modules (`Componente.module.css`)
  - Sin Tailwind ni librerías de utilidades CSS
- **Gestor de paquetes:** pnpm (no usar npm ni yarn — mantener un solo lockfile consistente)

## Comandos
- Instalar dependencias: `pnpm install`
- Desarrollo local: `pnpm dev`
- Build de producción: `pnpm build`
- Preview del build: `pnpm preview`

## Estructura de carpetas
```
project-root/
├── public/                    → assets estáticos servidos tal cual (favicon, robots.txt, og-image.png)
├── src/
│   ├── assets/                 → imágenes fuente (Astro las optimiza automáticamente vía astro:assets)
│   ├── components/
│   │   ├── Hero/Hero.astro
│   │   ├── Navbar/
│   │   │   ├── Navbar.tsx
│   │   │   └── Navbar.module.css
│   │   ├── Features/Features.astro
│   │   ├── Testimonials/Testimonials.astro
│   │   ├── CTA/CTA.astro
│   │   └── Footer/Footer.astro
│   ├── layouts/
│   │   └── BaseLayout.astro    → <head>, meta tags, SEO, Open Graph, favicon
│   ├── pages/
│   │   └── index.astro         → importa y ordena las secciones
│   └── styles/
│       └── global.css          → reset CSS, variables de diseño (colores, tipografía, espaciado)
├── astro.config.mjs
├── package.json
└── AGENTS.md
```

**Convención de nombres:** PascalCase para archivos y carpetas de componentes (`Hero.astro`, `Navbar.tsx`). Cada componente vive en su propia carpeta junto con su CSS cuando corresponde (React islands).

## Convenciones de código
- Componentes `.astro`: un solo archivo con markup + `<style>` scoped juntos — no fragmentar innecesariamente en múltiples archivos.
- Componentes React: CSS Modules para estilos, clases en camelCase dentro del módulo.
- Variables de diseño (colores, spacing, tipografía) centralizadas como CSS custom properties en `src/styles/global.css` y reutilizadas en todos los componentes. Nunca hardcodear un color o tamaño repetido en múltiples archivos sueltos.

## Mobile-first / responsive
- Diseñar primero para mobile (375px de referencia), escalar hacia arriba.
- Breakpoints: 480px (mobile grande), 768px (tablet), 1024px (desktop).
- Usar `min-width` en media queries (mobile-first real), no `max-width` como base.

## Accesibilidad
- HTML semántico obligatorio: `<header>`, `<nav>`, `<main>`, `<section>`, `<footer>`. Nada de `<div>` genérico donde exista una etiqueta semántica apropiada.
- Todas las imágenes con `alt` descriptivo.
- Contraste de color mínimo AA (4.5:1 para texto normal).
- Elementos interactivos navegables por teclado, con estado de foco visible.

## SEO técnico
- Title y meta description únicos y descriptivos.
- Favicon configurado.
- Open Graph tags (`og:title`, `og:description`, `og:image`) para compartir en redes.
- Un solo `<h1>` por página.
- URLs limpias, sin parámetros innecesarios.

## Performance / imágenes
- Todas las imágenes van en `src/assets/` y se renderizan con el componente `<Image />` de `astro:assets` — Astro las optimiza automáticamente (resize, conversión a WebP/AVIF, lazy loading) durante el build. No hace falta comprimirlas manualmente, pero evitar subir fuente sin ningún criterio de tamaño.
- Nada de librerías JS pesadas para animaciones simples — usar CSS cuando alcance.

## Deploy
- Target: Vercel.
- Build command: `pnpm build`, output directory: `dist/`.
- No se requieren variables de entorno para este proyecto.

## Restricciones
- Seguir fielmente la referencia visual indicada en el brief de cada proyecto (paleta, tipografía, layout, jerarquía visual) — el objetivo es que el resultado final se vea como esa referencia, adaptando el contenido al rubro correspondiente.
- No usar frameworks, librerías o dependencias pesadas sin justificación (nada de CMS, backend, ni paquetes innecesarios para una landing estática).
- No generar información real verificable (direcciones, teléfonos, emails reales) — todo el contenido es ficticio, exclusivamente para portfolio.

## Checklist antes de dar por terminado
- [ ] Responsive probado en mobile y desktop
- [ ] Sin errores en consola del navegador
- [ ] Todas las imágenes con alt
- [ ] Un solo h1 por página
- [ ] Meta tags y Open Graph completos
- [ ] Lighthouse (performance y accesibilidad) revisado