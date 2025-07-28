# PROMPT 002: Configurar estructura de carpetas escalable según arquitectura hexagonal

## CONTEXTO DEL PROYECTO
Continuando con la plataforma de restaurantes tipo "Uber Eats meets Yelp", ahora necesitamos crear una estructura de carpetas empresarial que soporte:
- Sistema multi-usuario (público, restaurantes, superadmin)
- Simulador colaborativo en tiempo real
- Integración con múltiples APIs (Google, OpenAI, Stripe)
- Sistema de métricas y analytics
- Arquitectura escalable para 500+ componentes

## OBJETIVO ESPECÍFICO
Crear una estructura de carpetas robusta basada en arquitectura hexagonal que permita escalabilidad, mantenibilidad y separación clara de responsabilidades.

## INSTRUCCIONES DETALLADAS

### 1. ESTRUCTURA PRINCIPAL EN /src
```
src/
├── app/                     # Next.js 14 App Router
├── components/              # Componentes React reutilizables
├── lib/                     # Configuraciones y utilidades core
├── types/                   # Definiciones TypeScript globales
├── hooks/                   # Custom hooks reutilizables
├── stores/                  # Estado global (Zustand/Redux)
├── services/                # Servicios de negocio (Arquitectura Hexagonal)
├── adapters/                # Adaptadores para APIs externas
├── repositories/            # Capa de acceso a datos
├── domain/                  # Lógica de dominio pura
├── infrastructure/          # Implementaciones técnicas
├── utils/                   # Funciones utilitarias puras
├── constants/              # Constantes de la aplicación
├── schemas/                # Esquemas de validación (Zod)
├── styles/                 # Estilos globales y temas
└── middleware/             # Middlewares personalizados
```

### 2. ESTRUCTURA DETALLADA DE /app (Next.js App Router)
```
src/app/
├── (auth)/                 # Grupo de rutas de autenticación
│   ├── login/
│   │   └── page.tsx
│   ├── register/
│   │   └── page.tsx
│   ├── forgot-password/
│   │   └── page.tsx
│   └── layout.tsx
├── (dashboard)/           # Grupo de rutas del dashboard
│   ├── admin/
│   │   ├── analytics/
│   │   ├── restaurants/
│   │   ├── users/
│   │   └── layout.tsx
│   └── restaurant/
│       ├── menu/
│       ├── analytics/
│       ├── profile/
│       └── layout.tsx
├── (public)/              # Grupo de rutas públicas
│   ├── search/
│   │   └── page.tsx
│   ├── restaurant/
│   │   └── [id]/
│   │       ├── page.tsx
│   │       └── menu/
│   └── events/
├── api/                   # API Routes
│   ├── auth/
│   ├── restaurants/
│   ├── dishes/
│   ├── tickets/
│   ├── analytics/
│   ├── uploads/
│   └── webhooks/
├── globals.css
├── layout.tsx
├── page.tsx
├── loading.tsx
├── error.tsx
├── not-found.tsx
└── offline.tsx
```

### 3. ESTRUCTURA DETALLADA DE /components
```
src/components/
├── ui/                    # Componentes base reutilizables
│   ├── button.tsx
│   ├── input.tsx
│   ├── modal.tsx
│   ├── card.tsx
│   ├── badge.tsx
│   ├── avatar.tsx
│   ├── spinner.tsx
│   ├── skeleton.tsx
│   ├── toast.tsx
│   └── index.ts
├── forms/                 # Componentes de formularios
│   ├── auth/
│   ├── restaurant/
│   ├── dish/
│   └── user/
├── layout/                # Componentes de layout
│   ├── header.tsx
│   ├── footer.tsx
│   ├── sidebar.tsx
│   ├── navigation.tsx
│   └── breadcrumb.tsx
├── features/              # Componentes por feature
│   ├── search/
│   │   ├── search-bar.tsx
│   │   ├── filter-panel.tsx
│   │   ├── results-grid.tsx
│   │   └── index.ts
│   ├── restaurant/
│   │   ├── profile-card.tsx
│   │   ├── menu-display.tsx
│   │   ├── image-gallery.tsx
│   │   └── index.ts
│   ├── ticket-simulator/
│   │   ├── collaborative-ticket.tsx
│   │   ├── diner-selector.tsx
│   │   ├── dish-adder.tsx
│   │   └── index.ts
│   ├── analytics/
│   └── admin/
├── providers/             # Context providers
│   ├── auth-provider.tsx
│   ├── theme-provider.tsx
│   ├── socket-provider.tsx
│   └── query-provider.tsx
└── shared/                # Componentes compartidos específicos
    ├── maps/
    ├── upload/
    ├── charts/
    └── notifications/
```

### 4. ESTRUCTURA DE /lib (Configuraciones Core)
```
src/lib/
├── auth/
│   ├── config.ts
│   ├── jwt.ts
│   └── session.ts
├── database/
│   ├── prisma.ts
│   ├── redis.ts
│   └── migrations/
├── external-apis/
│   ├── google/
│   │   ├── places.ts
│   │   └── maps.ts
│   ├── openai/
│   │   ├── vision.ts
│   │   └── translations.ts
│   ├── stripe/
│   │   └── payments.ts
│   └── socket/
│       └── config.ts
├── validations/
│   ├── auth.ts
│   ├── restaurant.ts
│   ├── dish.ts
│   └── user.ts
├── cache/
│   ├── redis-config.ts
│   ├── strategies.ts
│   └── invalidation.ts
├── security/
│   ├── rate-limit.ts
│   ├── cors.ts
│   └── sanitization.ts
├── monitoring/
│   ├── logging.ts
│   ├── analytics.ts
│   └── error-tracking.ts
└── utils/
    ├── cn.ts
    ├── formatters.ts
    ├── validators.ts
    └── constants.ts
```

### 5. ESTRUCTURA DE /services (Arquitectura Hexagonal)
```
src/services/
├── auth/
│   ├── auth.service.ts
│   ├── auth.interface.ts
│   └── auth.types.ts
├── restaurant/
│   ├── restaurant.service.ts
│   ├── restaurant.interface.ts
│   └── restaurant.types.ts
├── dish/
│   ├── dish.service.ts
│   ├── dish.interface.ts
│   └── dish.types.ts
├── ticket/
│   ├── ticket.service.ts
│   ├── collaborative-ticket.service.ts
│   └── ticket.types.ts
├── search/
│   ├── search.service.ts
│   ├── geo-location.service.ts
│   └── filters.service.ts
├── analytics/
│   ├── metrics.service.ts
│   ├── reporting.service.ts
│   └── tracking.service.ts
├── ai/
│   ├── menu-processing.service.ts
│   ├── translation.service.ts
│   └── recommendations.service.ts
├── notification/
│   ├── email.service.ts
│   ├── push.service.ts
│   └── sms.service.ts
└── payment/
    ├── subscription.service.ts
    └── billing.service.ts
```

### 6. ESTRUCTURA DE /types (TypeScript Definitions)
```
src/types/
├── auth.types.ts
├── restaurant.types.ts
├── dish.types.ts
├── user.types.ts
├── ticket.types.ts
├── analytics.types.ts
├── api.types.ts
├── database.types.ts
├── external-apis.types.ts
├── ui.types.ts
├── form.types.ts
├── websocket.types.ts
└── global.d.ts
```

### 7. ESTRUCTURA DE /hooks
```
src/hooks/
├── auth/
│   ├── use-auth.ts
│   ├── use-session.ts
│   └── use-permissions.ts
├── data/
│   ├── use-restaurants.ts
│   ├── use-dishes.ts
│   ├── use-search.ts
│   └── use-analytics.ts
├── ui/
│   ├── use-modal.ts
│   ├── use-toast.ts
│   ├── use-pagination.ts
│   └── use-infinite-scroll.ts
├── ticket/
│   ├── use-collaborative-ticket.ts
│   ├── use-ticket-sync.ts
│   └── use-diner-management.ts
├── geolocation/
│   ├── use-location.ts
│   └── use-distance-calculator.ts
└── shared/
    ├── use-debounce.ts
    ├── use-local-storage.ts
    ├── use-websocket.ts
    └── use-api.ts
```

### 8. ESTRUCTURA DE /stores (Estado Global)
```
src/stores/
├── auth/
│   ├── auth.store.ts
│   └── session.store.ts
├── restaurant/
│   └── restaurant.store.ts
├── ticket/
│   ├── ticket.store.ts
│   └── collaborative.store.ts
├── search/
│   ├── filters.store.ts
│   └── results.store.ts
├── ui/
│   ├── modal.store.ts
│   ├── toast.store.ts
│   └── theme.store.ts
├── cache/
│   └── cache.store.ts
└── index.ts
```

### 9. CREAR ARCHIVOS INDEX PARA EXPORTS LIMPIOS
En cada carpeta principal, crear `index.ts`:

**components/ui/index.ts:**
```typescript
export { Button } from './button'
export { Input } from './input'
export { Modal } from './modal'
export { Card } from './card'
// ... más exports
```

**services/index.ts:**
```typescript
export * from './auth/auth.service'
export * from './restaurant/restaurant.service'
export * from './dish/dish.service'
// ... más exports
```

### 10. CONFIGURAR ALIAS EN tsconfig.json
Actualizar paths en tsconfig.json:
```json
{
  "compilerOptions": {
    "paths": {
      "@/*": ["./src/*"],
      "@/components/*": ["./src/components/*"],
      "@/ui": ["./src/components/ui"],
      "@/lib/*": ["./src/lib/*"],
      "@/types/*": ["./src/types/*"],
      "@/hooks/*": ["./src/hooks/*"],
      "@/services/*": ["./src/services/*"],
      "@/stores/*": ["./src/stores/*"],
      "@/utils/*": ["./src/utils/*"],
      "@/adapters/*": ["./src/adapters/*"],
      "@/domain/*": ["./src/domain/*"],
      "@/schemas/*": ["./src/schemas/*"]
    }
  }
}
```

### 11. CREAR ARCHIVOS .gitkeep
En carpetas vacías que necesitamos mantener:
```bash
touch src/adapters/.gitkeep
touch src/repositories/.gitkeep
touch src/domain/.gitkeep
touch src/infrastructure/.gitkeep
```

### 12. DOCUMENTAR ESTRUCTURA
Crear `ARCHITECTURE.md` en raíz del proyecto explicando la arquitectura hexagonal implementada.

## CRITERIOS DE ÉXITO
✅ Estructura de carpetas completa y organizada
✅ Separación clara de responsabilidades
✅ Alias de TypeScript configurados
✅ Archivos index para exports limpios
✅ Preparado para arquitectura hexagonal
✅ Escalable para 500+ componentes
✅ Estructura compatible con Next.js 14 App Router
✅ Organización por features y capas

## PRÓXIMO PASO
Una vez completado, procederemos con la **Tarea 003: Instalar y configurar ESLint con reglas strict para TypeScript**