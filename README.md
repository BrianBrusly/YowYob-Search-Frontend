# YowYob Search — Frontend (Next.js • PWA • SSR • SEO • Tailwind • Maps • OMS Tiles)
Interface moderne, rapide et optimisée du moteur de recherche intelligent YowYob Search.
Construit avec Next.js App Router, React Server Components, Tailwind, SSR, SEO avancé, PWA, Web Push Notifications, Web Analytics, OMS Tiles, Merchant Dashboard, User Dashboard, et intégration directe avec l'API Gateway backend.

> **Application de recherche intelligente progressive** - PWA moderne construite avec Next.js 14, TypeScript et Tailwind CSS offrant une expérience de recherche unifiée et performante

[![Next.js](https://img.shields.io/badge/Next.js-14-black.svg)](https://nextjs.org/)
[![TypeScript](https://img.shields.io/badge/TypeScript-5-blue.svg)](https://www.typescriptlang.org/)
[![PWA](https://img.shields.io/badge/PWA-✓-lightgrey.svg)](https://web.dev/progressive-web-apps/)
[![License](https://img.shields.io/badge/license-MIT-blue.svg)](LICENSE)


## Architecture et Vue d'Ensemble

Le frontend YowYob constitue l'interface utilisateur principale du moteur de recherche, orchestrant l'interaction entre les différents services backend et fournissant une expérience utilisateur fluide et réactive.

Le frontend YowYob Search PWA est une application web hautement optimisée, capable de fonctionner :
- comme site web classique (SSR)
- comme application mobile PWA (offline support)
- comme application installable sur desktop et mobile
- avec SEO maximal (indexation Google)
- comme UI unifiée pour utilisateurs, marchands, webmasters et administrateurs.

Il remplace Google Search avec une couche d'intelligence supplémentaire :

- résultats enrichis (aggregated shopping, maps, local businesses, analytics)
- comparaison de prix
- recommandations
- trending searches
- résultats géolocalisés
- notifications intelligentes

## Fonctionnalités Principales

### Recherche Intelligente (SSR + RSC)
- Autocomplétion et suggestions en temps réel  
- Résultats enrichis : snippet, images, prix, localisation  
- Mise en cache via Next.js et Edge Runtime  
- Requêtes server-side pour éviter l'exposition de l'API Gateway  

### OMS Tiles & Maps
- Support OpenStreetMap et tuiles interactives  
- Localisation en temps réel (HTML Geolocation API)  
- Recherche géolocalisée (GeoService + SearchService)  
- Résultats affichés sur carte (commerces, produits, entreprises)  

### Comparaison de Prix & Shopping
- Listing agrégé depuis le ShopService  
- Comparaison de prix marchands  
- Suivi des clics et redirections  
- Interface e-commerce optimisée  

### Analytics & Statistiques en Temps Réel
- Tracking complet : requêtes, clics, redirections, temps passé  
- SSE ou WebSocket pour dashboards marchands & webmasters  
- Indicateurs d'engagement et de performance  

### Notifications Intelligentes (Web Push)
- Installation automatique du service worker  
- Suggestions personnalisées  
- Alertes prix bas et produits tendances  
- Gestion multi-canaux  

### PWA Complète
- Recherche hors-ligne via cache local  
- Progressive images et lazy loading  
- Installation native (A2HS)  
- Performance optimisée  

### SEO Avancé
- Balises meta dynamiques et indexation multi-langues  
- Open Graph tags automatiques et sitemap dynamique  
- Données structurées (JSON-LD) pour produits  

### Dashboard Marchands / Utilisateurs / Webmasters
- KPI fournis par le StatsService en temps réel  
- Graphiques interactifs et tendances  
- Mesures : CTR, ROI, vues, clics, impressions  

### Authentification JWT
- Login / Register sécurisé  
- Session stockée en cookies HttpOnly  
- Auto-refresh du token  
- Protection des routes /dashboard  


### Connexion avec l'Architecture Globale

```
┌─────────────────────────────────────────────────────────────┐
│                    ÉCOSYSTÈME YOWYOB COMPLET               │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  ┌─────────────────────────────────────────────────────┐   │
│  │                  YOWYOB FRONTEND                    │   │
│  │                 (Next.js 14 - PWA)                  │   │
│  │                                                     │   │
│  │  ┌─────────────┐  ┌─────────────┐  ┌─────────────┐  │   │
│  │  │   Search    │  │   Geo       │  │   User      │  │   │
│  │  │  Interface  │  │  Services   │  │  Services   │  │   │
│  │  └─────────────┘  └─────────────┘  └─────────────┘  │   │
│  │                                                     │   │
│  │  ┌─────────────┐  ┌─────────────┐  ┌─────────────┐  │   │
│  │  │   Shop      │  │  Analytics  │  │ Notification│  │   │
│  │  │  Interface  │  │  Dashboard  │  │   Center    │  │   │
│  │  └─────────────┘  └─────────────┘  └─────────────┘  │   │
│  └─────────────────────────────────────────────────────┘   │
│                             │                              │
│                             ▼                              │
│  ┌─────────────────────────────────────────────────────┐   │
│  │               API GATEWAY (Backend)                 │   │
│  └─────────────────────────────────────────────────────┘   │
│                             │                              │
└─────────────────────────────────────────────────────────────┘
```

## Structure Détaillée du Projet

```
yowyob-search-frontend/
├── 📁 public/                          
│   ├── 📄 manifest.json               
│   ├── 📄 sw.js                      
│   ├── 📄 offline.html                
│   ├── 📁 icons/                      
│   └── 📁 images/                     # Images statiques optimisées
│
├── 📁 src/
│   ├── 📁 app/                        # App Router Next.js 14+
│   │   ├── 📁 (home)/                 # Page d'accueil avec layout racine
│   │   │   ├── 📄 page.tsx            
│   │   │   ├── 📄 layout.tsx          
│   │   │   └── 📄 loading.tsx         
│   │   │
│   │   ├── 📁 search/                 # Route principale de recherche
│   │   │   ├── 📄 page.tsx            
│   │   │   ├── 📄 layout.tsx          
│   │   │   ├── 📄 loading.tsx         
│   │   │   └── 📄 error.tsx           
│   │   │
│   │   ├── 📁 map/                    # Vue carte interactive
│   │   │   ├── 📄 page.tsx            
│   │   │   └── 📄 layout.tsx          
│   │   │
│   │   ├── 📁 products/               # Recherche produits e-commerce
│   │   │   ├── 📄 page.tsx            
│   │   │   └── 📁 [category]/         
│   │   │
│   │   ├── 📁 auth/                   # Authentification
│   │   │   ├── 📁 login/
│   │   │   ├── 📁 register/
│   │   │   └── 📁 forgot-password/
│   │   │
│   │   ├── 📁 profile/                # Gestion profil utilisateur
│   │   │   ├── 📄 page.tsx            
│   │   │   ├── 📁 history/            # Historique recherches
│   │   │   ├── 📁 preferences/        # Préférences utilisateur
│   │   │   └── 📁 saved/              # Recherches sauvegardées
│   │   │
│   │   ├── 📁 merchant/               # Interface marchands
│   │   │   ├── 📄 page.tsx            
│   │   │   ├── 📁 analytics/          # Statistiques marchand
│   │   │   └── 📁 products/           # Gestion produits
│   │   │
│   │   └── 📁 admin/                  # Interface administrateur
│   │       ├── 📄 page.tsx            
│   │       ├── 📁 dashboard/          
│   │       ├── 📁 users/              
│   │       └── 📁 system/             
│   │
│   ├── 📁 components/                 
│   │   ├── 📁 ui/                     # Composants d'interface réutilisables
│   │   │   ├── 📄 button.tsx          
│   │   │   ├── 📄 input.tsx           
│   │   │   ├── 📄 select.tsx          
│   │   │   ├── 📄 dialog.tsx          
│   │   │   ├── 📄 card.tsx            
│   │   │   ├── 📄 badge.tsx           
│   │   │   ├── 📄 avatar.tsx          
│   │   │   ├── 📄 tooltip.tsx         
│   │   │   ├── 📄 dropdown.tsx        
│   │   │   ├── 📄 tabs.tsx            
│   │   │   ├── 📄 accordion.tsx       
│   │   │   ├── 📄 skeleton.tsx        
│   │   │   ├── 📄 progress.tsx        
│   │   │   ├── 📄 toast.tsx           
│   │   │   └── 📄 breadcrumb.tsx      
│   │   │
│   │   ├── 📁 layout/                 # Composants de mise en page
│   │   │   ├── 📄 header.tsx          
│   │   │   ├── 📄 footer.tsx          
│   │   │   ├── 📄 sidebar.tsx         
│   │   │   ├── 📄 navigation.tsx      
│   │   │   ├── 📄 mobile-nav.tsx      
│   │   │   ├── 📄 search-header.tsx   # Header spécialisé recherche
│   │   │   └── 📄 app-shell.tsx       # Shell principal PWA
│   │   │
│   │   ├── 📁 search/                 # Écosystème recherche
│   │   │   ├── 📄 search-bar.tsx      # Barre recherche principale
│   │   │   ├── 📄 search-suggestions.tsx 
│   │   │   ├── 📄 search-filters.tsx  
│   │   │   ├── 📄 advanced-filters.tsx 
│   │   │   ├── 📄 results-container.tsx 
│   │   │   ├── 📄 results-list.tsx    
│   │   │   ├── 📄 results-grid.tsx    
│   │   │   ├── 📄 result-card.tsx     
│   │   │   ├── 📄 result-skeleton.tsx 
│   │   │   ├── 📄 pagination.tsx      
│   │   │   ├── 📄 no-results.tsx      
│   │   │   ├── 📄 search-history.tsx  
│   │   │   ├── 📄 trending-searches.tsx 
│   │   │   └── 📄 search-analytics.tsx 
│   │   │
│   │   ├── 📁 map/                    # Composants cartographiques
│   │   │   ├── 📄 map-container.tsx   
│   │   │   ├── 📄 map-controls.tsx    
│   │   │   ├── 📄 map-layers.tsx      
│   │   │   ├── 📄 map-marker.tsx      
│   │   │   ├── 📄 map-cluster.tsx     
│   │   │   ├── 📄 map-popup.tsx       
│   │   │   ├── 📄 location-picker.tsx 
│   │   │   └── 📄 geo-suggestions.tsx 
│   │   │
│   │   ├── 📁 products/               # Composants e-commerce
│   │   │   ├── 📄 product-card.tsx    
│   │   │   ├── 📄 product-grid.tsx    
│   │   │   ├── 📄 product-filters.tsx 
│   │   │   ├── 📄 price-comparison.tsx 
│   │   │   ├── 📄 merchant-badge.tsx  
│   │   │   ├── 📄 rating-display.tsx  
│   │   │   ├── 📄 product-details.tsx 
│   │   │   └── 📄 cart-preview.tsx    
│   │   │
│   │   ├── 📁 auth/                   
│   │   │   ├── 📄 login-form.tsx      
│   │   │   ├── 📄 register-form.tsx   
│   │   │   ├── 📄 auth-provider.tsx   
│   │   │   └── 📄 protected-route.tsx 
│   │   │
│   │   ├── 📁 user/                   # Gestion utilisateur
│   │   │   ├── 📄 profile-form.tsx    
│   │   │   ├── 📄 preferences-form.tsx 
│   │   │   ├── 📄 subscription-card.tsx 
│   │   │   └── 📄 activity-feed.tsx   
│   │   │
│   │   ├── 📁 merchant/               # Interface marchands
│   │   │   ├── 📄 dashboard-stats.tsx 
│   │   │   ├── 📄 product-manager.tsx 
│   │   │   ├── 📄 analytics-chart.tsx 
│   │   │   └── 📄 performance-metrics.tsx 
│   │   │
│   │   └── 📁 pwa/                    # Fonctionnalités PWA
│   │       ├── 📄 install-prompt.tsx  
│   │       ├── 📄 offline-indicator.tsx 
│   │       ├── 📄 push-manager.tsx    
│   │       ├── 📄 sync-manager.tsx    
│   │       └── 📄 cache-manager.tsx   
│   │
│   ├── 📁 lib/                        
│   │   ├── 📁 api/                    # Clients et services API
│   │   │   ├── 📄 http-client.ts      # Client HTTP configuré
│   │   │   ├── 📄 search-service.ts   # Service recherche
│   │   │   ├── 📄 geo-service.ts      # Service géolocalisation
│   │   │   ├── 📄 user-service.ts     # Service utilisateur
│   │   │   ├── 📄 product-service.ts  # Service produits
│   │   │   ├── 📄 notification-service.ts 
│   │   │   ├── 📄 analytics-service.ts 
│   │   │   └── 📄 merchant-service.ts 
│   │   │
│   │   ├── 📁 hooks/                  # Custom React Hooks
│   │   │   ├── 📁 search/
│   │   │   │   ├── 📄 use-search.ts   
│   │   │   │   ├── 📄 use-suggestions.ts 
│   │   │   │   ├── 📄 use-search-history.ts 
│   │   │   │   └── 📄 use-search-analytics.ts 
│   │   │   │
│   │   │   ├── 📁 geo/
│   │   │   │   ├── 📄 use-geolocation.ts 
│   │   │   │   ├── 📄 use-map-interaction.ts 
│   │   │   │   └── 📄 use-address-suggestions.ts 
│   │   │   │
│   │   │   ├── 📁 user/
│   │   │   │   ├── 📄 use-auth.ts     
│   │   │   │   ├── 📄 use-user-profile.ts 
│   │   │   │   └── 📄 use-preferences.ts 
│   │   │   │
│   │   │   ├── 📁 products/
│   │   │   │   ├── 📄 use-product-search.ts 
│   │   │   │   ├── 📄 use-price-comparison.ts 
│   │   │   │   └── 📄 use-product-tracking.ts 
│   │   │   │
│   │   │   ├── 📁 ui/
│   │   │   │   ├── 📄 use-debounce.ts 
│   │   │   │   ├── 📄 use-infinite-scroll.ts 
│   │   │   │   ├── 📄 use-local-storage.ts 
│   │   │   │   ├── 📄 use-online-status.ts 
│   │   │   │   └── 📄 use-theme.ts    
│   │   │   │
│   │   │   └── 📁 pwa/
│   │   │       ├── 📄 use-push-notifications.ts 
│   │   │       ├── 📄 use-service-worker.ts 
│   │   │       └── 📄 use-offline-cache.ts 
│   │   │
│   │   ├── 📁 utils/                  
│   │   │   ├── 📄 formatters.ts       # Formatage données
│   │   │   ├── 📄 validators.ts       # Validation formulaires
│   │   │   ├── 📄 search-utils.ts     # Utilitaires recherche
│   │   │   ├── 📄 geo-utils.ts        # Utilitaires géo
│   │   │   ├── 📄 product-utils.ts    # Utilitaires produits
│   │   │   ├── 📄 storage.ts          # Gestion stockage
│   │   │   ├── 📄 seo.ts              # Optimisation SEO
│   │   │   ├── 📄 analytics.ts        # Analytics
│   │   │   └── 📄 error-handler.ts    # Gestion erreurs
│   │   │
│   │   ├── 📁 constants/              
│   │   │   ├── 📄 routes.ts           
│   │   │   ├── 📄 api-endpoints.ts    
│   │   │   ├── 📄 search-config.ts    
│   │   │   ├── 📄 map-config.ts       
│   │   │   ├── 📄 product-categories.ts 
│   │   │   └── 📄 app-config.ts       
│   │   │
│   │   └── 📁 providers/              # Context Providers
│   │       ├── 📄 theme-provider.tsx  
│   │       ├── 📄 auth-provider.tsx   
│   │       ├── 📄 search-provider.tsx 
│   │       ├── 📄 geo-provider.tsx    
│   │       └── 📄 app-provider.tsx    
│   │
│   ├── 📁 store/                      # State Management (Zustand)
│   │   ├── 📄 index.ts                
│   │   ├── 📁 slices/                 
│   │   │   ├── 📄 search-slice.ts     
│   │   │   ├── 📄 auth-slice.ts       
│   │   │   ├── 📄 ui-slice.ts         
│   │   │   ├── 📄 geo-slice.ts        
│   │   │   ├── 📄 product-slice.ts    
│   │   │   ├── 📄 notification-slice.ts 
│   │   │   └── 📄 merchant-slice.ts   
│   │   │
│   │   └── 📁 middleware/             
│   │       ├── 📄 persistence.ts      
│   │       ├── 📄 analytics.ts        
│   │       └── 📄 sync.ts             
│   │
│   ├── 📁 types/                      
│   │   ├── 📄 api.ts                  
│   │   ├── 📄 search.ts               
│   │   ├── 📄 geo.ts                  
│   │   ├── 📄 user.ts                 
│   │   ├── 📄 products.ts             
│   │   ├── 📄 merchant.ts             
│   │   └── 📄 app.ts                  
│   │
│   └── 📁 styles/                     
│       ├── 📄 globals.css             
│       ├── 📄 components.css          
│       ├── 📁 themes/                 
│       │   ├── 📄 light.css           
│       │   ├── 📄 dark.css            
│       │   └── 📄 variables.css       
│       └── 📁 animations/             
│           ├── 📄 transitions.css     
│           └── 📄 keyframes.css       
│
├── 📁 e2e/                            # Tests end-to-end
│   ├── 📁 specs/                      
│   │   ├── 📄 search.spec.ts          
│   │   ├── 📄 auth.spec.ts            
│   │   ├── 📄 products.spec.ts        
│   │   └── 📄 navigation.spec.ts      
│   └── 📄 playwright.config.ts        
│
├── 📁 docs/                           # Documentation
│   ├── 📄 architecture.md             
│   ├── 📄 components.md               
│   ├── 📄 api-integration.md          
│   └── 📄 deployment.md               
│
├── 📄 next.config.mjs                 
├── 📄 tailwind.config.ts              
├── 📄 tsconfig.json                   
├── 📄 package.json                    
└── 📄 README.md                       
```

## Intégration avec les Services Backend

### Service de Recherche (Search Service)
**Port backend : 8082**

Le frontend interagit avec le service de recherche via les composants suivants :

- **SearchBar** : Envoie les requêtes de recherche au backend
- **SearchSuggestions** : Récupère les suggestions en temps réel
- **ResultsList/ResultsGrid** : Affiche les résultats formatés
- **SearchFilters** : Applique les filtres backend (date, type, langue)
- **SearchAnalytics** : Track les métriques de recherche

**Flux typique :**
```typescript
// Exemple d'intégration search service
const searchResults = await searchService.search({
  query: "restaurants Yaoundé",
  filters: {
    location: { lat: 3.8667, lng: 11.5167 },
    radius: 5,
    language: "fr"
  },
  pagination: { page: 0, size: 20 }
});
```

### Service Géolocalisation (Geo Service)
**Port backend : 8084**

Intégration via les composants cartographiques :

- **MapContainer** : Affiche les données géospatiales
- **LocationPicker** : Utilise le géocodage pour convertir adresses → coordonnées
- **GeoSearch** : Recherche par proximité géographique
- **AddressSuggestions** : Autocomplétion d'adresses

**Utilisation :**
```typescript
// Géocodage d'une adresse
const location = await geoService.geocode("Yaoundé, Cameroun");
// → { lat: 3.8667, lng: 11.5167, address: "..." }

// Recherche par proximité
const nearbyResults = await geoService.searchNearby({
  center: location,
  radius: 10,
  type: "restaurant"
});
```

### Service Utilisateur (User Service)
**Port backend : 8083**

Gestion de l'authentification et du profil :

- **AuthProvider** : Gère l'état d'authentification global
- **Login/Register Forms** : Interfaces d'authentification
- **UserProfile** : Gestion du profil utilisateur
- **PreferencesManager** : Sauvegarde des préférences

**Sécurité :**
- Tokens JWT stockés sécuritairement
- Refresh token automatique
- Gestion des permissions (USER, MERCHANT, ADMIN)

### Service E-commerce (Shop Service)
**Port backend : 8087**

Interface produits et marchands :

- **ProductSearch** : Recherche spécifique produits
- **PriceComparison** : Comparaison de prix entre marchands
- **MerchantDashboard** : Interface analytics marchands
- **ProductManagement** : Gestion catalogue produits

**Fonctionnalités :**
```typescript
// Recherche produits
const products = await productService.search({
  query: "smartphone samsung",
  filters: {
    priceRange: { min: 100000, max: 500000 },
    category: "electronics",
    merchants: ["merchant1", "merchant2"]
  }
});
```

### Service Analytics (Stats Service)
**Port backend : 8088**

Tracking et analytics :

- **AnalyticsDashboard** : Visualisation données utilisateur
- **MerchantAnalytics** : Statistiques performance marchands
- **SearchAnalytics** : Analyse comportement recherche
- **RealTimeMetrics** : Métriques temps réel

### Service Notifications (Notification Service)
**Port backend : 8086**

Gestion des notifications multi-canaux :

- **PushManager** : Abonnement aux notifications push
- **NotificationCenter** : Centre de notifications
- **AlertSystem** : Système d'alertes personnalisées

## Architecture Technique Détaillée

### Pattern de Composition des Composants

```typescript
// Exemple de composant search haut niveau
export function SearchInterface() {
  return (
    <SearchProvider>
      <div className="search-interface">
        <SearchHeader>
          <SearchBar />
          <QuickFilters />
        </SearchHeader>
        
        <SearchBody>
          <SearchSidebar>
            <AdvancedFilters />
            <LocationFilter />
            <SearchHistory />
          </SearchSidebar>
          
          <SearchResults>
            <ResultsViewSwitch />
            <ResultsList />
            <Pagination />
          </SearchResults>
        </SearchBody>
        
        <SearchAnalytics />
      </div>
    </SearchProvider>
  );
}
```

### Gestion d'État Avancée

```typescript
// Store search avec persistance et synchronisation
export const useSearchStore = create<SearchState>()(
  persist(
    (set, get) => ({
      // État
      query: '',
      results: [],
      filters: {},
      isLoading: false,
      
      // Actions
      setQuery: (query) => {
        set({ query });
        get().trackSearchQuery(query);
      },
      
      performSearch: async (params) => {
        set({ isLoading: true });
        
        try {
          const results = await searchService.search(params);
          set({ results, isLoading: false });
          get().trackSearchResults(results);
        } catch (error) {
          set({ isLoading: false, error: error.message });
        }
      },
      
      // Analytics intégrés
      trackSearchQuery: (query) => {
        analyticsService.track('search_query', { query });
      }
    }),
    {
      name: 'search-storage',
      partialize: (state) => ({ 
        query: state.query,
        filters: state.filters 
      })
    }
  )
);
```

### Système de Thèmes et Design Tokens

```typescript
// Configuration design system complète
export const designTokens = {
  colors: {
    primary: {
      50: '#f0f9ff',
      100: '#e0f2fe',
      // ... échelle complète
      900: '#0c4a6e'
    },
    semantic: {
      success: '#10b981',
      warning: '#f59e0b',
      error: '#ef4444'
    }
  },
  typography: {
    scales: {
      xs: { fontSize: '0.75rem', lineHeight: '1rem' },
      sm: { fontSize: '0.875rem', lineHeight: '1.25rem' },
      // ... échelles complètes
    }
  },
  spacing: {
    xs: '0.25rem',
    sm: '0.5rem',
    // ... échelle complète
  },
  breakpoints: {
    sm: '640px',
    md: '768px',
    lg: '1024px',
    xl: '1280px'
  }
};
```

## Performance et Optimisations

### Stratégies de Chargement

```typescript
// Loading stratégique avec React Suspense
export default function SearchPage() {
  return (
    <div className="search-page">
      <Suspense fallback={<SearchSkeleton />}>
        <SearchHeader />
      </Suspense>
      
      <div className="search-content">
        <Suspense fallback={<FiltersSkeleton />}>
          <SearchSidebar />
        </Suspense>
        
        <Suspense fallback={<ResultsSkeleton />}>
          <SearchResults />
        </Suspense>
      </div>
    </div>
  );
}
```

### Cache et Offline Strategy

```typescript
// Service Worker avancé avec stratégies de cache
const CACHE_STRATEGIES = {
  search: {
    pattern: /\/api\/search/,
    strategy: 'network-first',
    cacheName: 'search-cache',
    expiration: { maxEntries: 50, maxAgeSeconds: 3600 }
  },
  static: {
    pattern: /\.(js|css|png|jpg)/,
    strategy: 'cache-first',
    cacheName: 'static-cache'
  },
  api: {
    pattern: /\/api\//,
    strategy: 'stale-while-revalidate',
    cacheName: 'api-cache'
  }
};
```

## Sécurité et Bonnes Pratiques

### Protection des Données Sensibles

```typescript
// Gestion sécurisée des tokens
class SecureStorage {
  static setItem(key: string, value: string) {
    if (typeof window !== 'undefined') {
      // Chiffrement des données sensibles
      const encrypted = CryptoJS.AES.encrypt(
        value, 
        process.env.NEXT_PUBLIC_CRYPTO_KEY
      ).toString();
      localStorage.setItem(key, encrypted);
    }
  }
  
  static getItem(key: string): string | null {
    if (typeof window !== 'undefined') {
      const encrypted = localStorage.getItem(key);
      if (!encrypted) return null;
      
      try {
        const decrypted = CryptoJS.AES.decrypt(
          encrypted, 
          process.env.NEXT_PUBLIC_CRYPTO_KEY
        ).toString(CryptoJS.enc.Utf8);
        return decrypted;
      } catch {
        return null;
      }
    }
    return null;
  }
}
```

### Validation des Données

```typescript
// Schémas de validation complets avec Zod
export const SearchRequestSchema = z.object({
  query: z.string().min(1).max(500),
  filters: z.object({
    location: z.object({
      lat: z.number().min(-90).max(90),
      lng: z.number().min(-180).max(180)
    }).optional(),
    radius: z.number().min(1).max(100).optional(),
    dateRange: z.object({
      from: z.date().optional(),
      to: z.date().optional()
    }).optional()
  }).optional(),
  pagination: z.object({
    page: z.number().min(0),
    size: z.number().min(1).max(100)
  }).default({ page: 0, size: 20 })
});

export type SearchRequest = z.infer<typeof SearchRequestSchema>;
```

## Tests et Qualité

### Structure de Tests Complète

```typescript
// Tests d'intégration search
describe('Search Integration', () => {
  it('should perform search with filters', async () => {
    const { result } = renderHook(() => useSearch());
    
    await act(async () => {
      await result.current.performSearch({
        query: 'test query',
        filters: { location: { lat: 3.8667, lng: 11.5167 } }
      });
    });
    
    expect(result.current.results).toHaveLength(10);
    expect(result.current.isLoading).toBe(false);
  });
  
  it('should handle search errors gracefully', async () => {
    // Mock API error
    mockSearchService.search.mockRejectedValue(new Error('API Error'));
    
    const { result } = renderHook(() => useSearch());
    
    await act(async () => {
      await result.current.performSearch({ query: 'test' });
    });
    
    expect(result.current.error).toBe('API Error');
    expect(result.current.isLoading).toBe(false);
  });
});
```

## Déploiement et DevOps

### Configuration Multi-Environnement

```typescript
// Configuration environnement dynamique
export const getConfig = () => {
  const environment = process.env.NEXT_PUBLIC_APP_ENV || 'development';
  
  const configs = {
    development: {
      apiUrl: 'http://localhost:8080',
      analytics: false,
      debug: true
    },
    staging: {
      apiUrl: 'https://staging-api.yowyob.com',
      analytics: true,
      debug: true
    },
    production: {
      apiUrl: 'https://api.yowyob.com',
      analytics: true,
      debug: false
    }
  };
  
  return configs[environment];
};
```

### Métriques de Performance

```typescript
// Tracking des métriques Core Web Vitals
export const webVitalsTracker = (metric: any) => {
  const body = JSON.stringify(metric);
  navigator.sendBeacon('/api/analytics/web-vitals', body);
  
  // Log pour le développement
  if (process.env.NODE_ENV === 'development') {
    console.log(metric);
  }
};
```

Cette architecture frontend détaillée permet une intégration complète avec tous les services backend tout en maintenant une expérience utilisateur exceptionnelle, des performances optimales et une maintenabilité à long terme.

## 🏛️ Justifications Architecturales

### 1. **App Router Next.js 14+** (vs Pages Router)

**Pourquoi App Router ?**
-  **Server Components par défaut** : Meilleure performance, HTML pré-rendu serveur
-  **Streaming SSR** : Chargement progressif avec React Suspense
-  **Layouts imbriqués** : Réutilisation layout sans re-render
-  **Loading/Error UI** : Gestion états automatique
-  **Route Handlers** : API routes simplifiées

**Structure typique page :**
```typescript
// app/search/page.tsx (Server Component)
export default async function SearchPage({ searchParams }) {
  // Fetch côté serveur (SEO-friendly)
  const results = await fetchSearchResults(searchParams.q);
  
  return (
    <Suspense fallback={<ResultSkeleton />}>
      <SearchResults results={results} />
    </Suspense>
  );
}
```

### 2. **Organisation des Composants**

**`components/layout/` - Composants structurels**
- **Pourquoi séparer ?** Réutilisabilité travers pages
- **Pattern** : Composition (`<Layout><Header /><Sidebar /></Layout>`)

**`components/search/` - Composants domaine**
- **Principe SRP** : Chaque composant = UNE responsabilité
  - `SearchBar` : Input + validation
  - `SearchSuggestions` : Autocomplete
  - `SearchFilters` : Filtres UI
  - `ResultCard` : Présentation résultat

**`components/common/` - Composants réutilisables**
- **Design System** : Boutons, inputs, modals standardisés
- **Avantage** : Consistance UI + maintenabilité

### 3. **State Management : Zustand**

**Pourquoi Zustand (vs Redux/Context API) ?**
-  **Simplicité** : Pas de boilerplate
-  **Performance** : Re-renders optimisés
-  **TypeScript** : Type-safe natif
-  **DevTools** : Débogage facile

**Exemple Store :**
```typescript
// store/slices/searchSlice.ts
interface SearchState {
  query: string;
  results: SearchResult[];
  isLoading: boolean;
  setQuery: (query: string) => void;
  search: (query: string) => Promise<void>;
}

export const useSearchStore = create<SearchState>((set) => ({
  query: '',
  results: [],
  isLoading: false,
  
  setQuery: (query) => set({ query }),
  
  search: async (query) => {
    set({ isLoading: true });
    try {
      const results = await searchApi.search(query);
      set({ results, isLoading: false });
    } catch (error) {
      set({ isLoading: false });
    }
  },
}));
```

### 4. **Custom Hooks (`lib/hooks/`)**

**`useSearch.ts` - Hook recherche avec debounce**
```typescript
export function useSearch(initialQuery = '') {
  const [query, setQuery] = useState(initialQuery);
  const [results, setResults] = useState([]);
  const [isLoading, setIsLoading] = useState(false);
  
  // Debounce 300ms pour éviter requêtes excessives
  const debouncedQuery = useDebounce(query, 300);
  
  useEffect(() => {
    if (!debouncedQuery) return;
    
    const performSearch = async () => {
      setIsLoading(true);
      try {
        const data = await searchApi.search(debouncedQuery);
        setResults(data.results);
      } catch (error) {
        console.error('Search failed:', error);
      } finally {
        setIsLoading(false);
      }
    };
    
    performSearch();
  }, [debouncedQuery]);
  
  return { query, setQuery, results, isLoading };
}
```

**Pourquoi custom hooks ?**
-  **Réutilisabilité** : Logique partagée entre composants
-  **Testabilité** : Testable indépendamment
-  **Séparation préoccupations** : Logique hors composants UI

### 5. **API Client (`lib/api/`)**

**`client.ts` - Configuration Axios centralisée**
```typescript
const apiClient = axios.create({
  baseURL: process.env.NEXT_PUBLIC_API_URL,
  timeout: 10000,
});

// Intercepteur requête : Ajouter JWT
apiClient.interceptors.request.use((config) => {
  const token = localStorage.getItem('accessToken');
  if (token) {
    config.headers.Authorization = `Bearer ${token}`;
  }
  return config;
});

// Intercepteur réponse : Gestion erreurs + refresh token
apiClient.interceptors.response.use(
  (response) => response,
  async (error) => {
    if (error.response?.status === 401) {
      // Refresh token logic
    }
    return Promise.reject(error);
  }
);
```

**Pourquoi intercepteurs ?**
-  **DRY** : Pas de répétition logique auth dans chaque appel
-  **Gestion centralisée erreurs**
-  **Refresh token automatique**

### 6. **Progressive Web App (PWA)**

**`manifest.json` - Configuration PWA**
```json
{
  "name": "YowYob Search",
  "short_name": "YowYob",
  "start_url": "/",
  "display": "standalone",
  "theme_color": "#3b82f6",
  "icons": [...]
}
```

**Pourquoi PWA ?**
-  **Offline-first** : App fonctionnelle sans connexion
-  **Installable** : Icône écran d'accueil (A2HS)
-  **Push notifications** : Engagement utilisateur
-  **Performance** : Cache agressif

### 7. **TypeScript Types (`types/`)**

**`types/search.ts`**
```typescript
export interface SearchRequest {
  query: string;
  page?: number;
  size?: number;
  filters?: SearchFilters;
}

export interface SearchResult {
  id: string;
  title: string;
  snippet: string;
  url: string;
  score: number;
}
```

**Pourquoi TypeScript ?**
-  **Type safety** : Détection erreurs compilation
-  **IntelliSense** : Autocomplétion IDE
-  **Refactoring** : Sécurité lors modifications

---

##  Dépendances Critiques Frontend

### `package.json` essentiel :
```json
{
  "dependencies": {
    "next": "^14.2.0",
    "react": "^18.3.0",
    "react-dom": "^18.3.0",
    "axios": "^1.6.0",
    "zustand": "^4.5.0",
    "leaflet": "^1.9.4",
    "react-leaflet": "^4.2.1",
    "next-pwa": "^5.6.0",
    "react-hook-form": "^7.51.0",
    "zod": "^3.22.0"
  },
  "devDependencies": {
    "typescript": "^5.4.0",
    "tailwindcss": "^3.4.0",
    "@testing-library/react": "^14.2.0"
  }
}
```

### Justifications dépendances :

| Dépendance | Pourquoi ? |
|------------|------------|
| **next** | Framework React SSR/SSG/ISR |
| **axios** | HTTP client (vs fetch natif) pour intercepteurs |
| **zustand** | State management léger |
| **leaflet** | Cartes interactives OpenStreetMap |
| **next-pwa** | Configuration PWA automatique |
| **react-hook-form** | Gestion formulaires performante |
| **zod** | Validation schéma TypeScript |
| **tailwindcss** | Utility-first CSS |
| **date-fns** | Manipulation dates (vs moment.js obsolète) |

---

##  Principes SOLID Appliqués

### **S - Single Responsibility Principle**
- `SearchBar` : Uniquement input recherche
- `ResultCard` : Uniquement affichage résultat
- `useSearch` : Uniquement logique recherche

### **O - Open/Closed Principle**
```typescript
// Composant ouvert à extension
interface SearchFilterProps {
  filters: SearchFilters;
  onFiltersChange: (filters: SearchFilters) => void;
}

export function SearchFilters({ filters, onFiltersChange }: SearchFilterProps) {
  // Implémentation extensible
}
```

### **L - Liskov Substitution Principle**
```typescript
// Tous les composants bouton sont substituables
<Button variant="primary">Rechercher</Button>
<Button variant="secondary">Annuler</Button>
<Button variant="danger" disabled>Supprimer</Button>
```

### **I - Interface Segregation Principle**
```typescript
// Interfaces fines et ciblées
interface Searchable {
  search(query: string): Promise<SearchResult[]>;
}

interface Filterable {
  applyFilters(filters: SearchFilters): void;
}

interface Paginable {
  goToPage(page: number): void;
}
```

### **D - Dependency Inversion Principle**
```typescript
// Composants dépendent d'abstractions
interface ApiClient {
  search(request: SearchRequest): Promise<SearchResponse>;
}

function SearchResults({ apiClient }: { apiClient: ApiClient }) {
  // Utilise l'interface, pas l'implémentation
}
```

---

##  Avantages de cette Architecture

### **Performance**
-  **Server Components** : Réduction JavaScript client
-  **Code Splitting** : Chargement lazy des routes
-  **Image Optimization** : Next.js Image component
-  **PWA Cache** : Stratégies cache agressives

### **Maintenabilité**
-  **Separation of Concerns** : Logique bien séparée
-  **Type Safety** : TypeScript partout
-  **Composable** : Composants réutilisables
-  **Testable** : Structure facilitant les tests

### **Expérience Utilisateur**
-  **Offline First** : Fonctionnement sans connexion
-  **Installable** : Comme une app native
-  **Rapide** : Temps de chargement optimisés
-  **Accessible** : Respect WCAG 2.1 AA

### **Développeur Experience**
-  **Hot Reload** : Développement fluide
-  **TypeScript** : Autocomplétion et refactoring
-  **ESLint/Prettier** : Code consistent
-  **Error Boundaries** : Gestion erreurs élégante

---

## Évolution Future

### **Améliorations prévues**
1. **Internationalisation** (i18n) avec next-intl
2. **Analytics avancés** avec custom events
3. **Tests E2E** avec Playwright
4. **Performance monitoring** avec Web Vitals
5. **A/B Testing** infrastructure

### **Scalabilité**
-  **Micro-frontends** si nécessaire
-  **CDN** pour assets statiques
-  **Edge Computing** avec Vercel Edge Functions
-  **Monitoring** avec OpenTelemetry

**Cette architecture frontend garantit une base solide, performante et maintenable pour YowYob Search, alignée avec les meilleures pratiques modernes de développement web.**


### Architecture globale

```
┌─────────────────────────────────────────────────────────────┐
│                    YOWYOB FRONTEND ARCHITECTURE             │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  ┌─────────────────┐    ┌─────────────────┐    ┌─────────┐  │
│  │   Next.js 14    │    │   State Mgmt    │    │   PWA   │  │
│  │   App Router    │◄──►│   (Zustand)     │◄──►│  Cache  │  │
│  └─────────────────┘    └─────────────────┘    └─────────┘  │
│         │                           │              │        │
│         │                           │              │        │
│         ▼                           ▼              ▼        │
│  ┌─────────────────┐    ┌─────────────────┐    ┌─────────┐  │
│  │   Components    │    │   Custom Hooks  │    │ Service │  │
│  │   Hierarchy     │    │   & Utilities   │    │ Worker  │  │
│  └─────────────────┘    └─────────────────┘    └─────────┘  │
│         │                           │              │        │
│         └─────────────┬─────────────┘              │        │
│                       │                            │        │
│                       ▼                            ▼        │
│                ┌─────────────┐              ┌─────────────┐ │
│                │   API Layer │◄─────────────│   Backend   │ │
│                │  (Axios)    │              │  Services   │ │
│                └─────────────┘              └─────────────┘ │
│                                                             │
└─────────────────────────────────────────────────────────────┘
```

###  Flux de données

```
Utilisateur → Composant UI → Custom Hook → Store (Zustand) → API Client → Backend
      │            │             │             │               │           │
      │            │             │             │               │           │
      ◄────────────◄─────────────◄─────────────◄───────────────◄───────────┘
      (Mise à jour UI via Reactivity)
```

---

##Stack technique

### Core Framework
- **Next.js 14** avec App Router
- **React 18** avec Server Components
- **TypeScript 5** pour la type-safety
- **Tailwind CSS** pour le styling

### State Management
- **Zustand** pour le state global léger
- **React Hook Form** pour les formulaires
- **Zod** pour la validation de schémas

### Cartographie
- **Leaflet** pour les cartes interactives
- **React Leaflet** pour l'intégration React
- **OpenStreetMap** pour les données carto

### PWA & Performance
- **next-pwa** pour la configuration PWA
- **Service Worker** pour le cache offline
- **Web Push API** pour les notifications
- **Lazy Loading** pour le code splitting

### Développement & Qualité
- **ESLint** + **Prettier** pour le code quality
- **Jest** + **Testing Library** pour les tests
- **Playwright** pour les tests E2E
- **Husky** pour les git hooks

### Dépendances principales

```json
{
  "dependencies": {
    "next": "^14.2.0",
    "react": "^18.3.0",
    "react-dom": "^18.3.0",
    "typescript": "^5.4.0",
    "tailwindcss": "^3.4.0",
    "axios": "^1.6.0",
    "zustand": "^4.5.0",
    "leaflet": "^1.9.4",
    "react-leaflet": "^4.2.1",
    "next-pwa": "^5.6.0",
    "react-hook-form": "^7.51.0",
    "zod": "^3.22.0",
    "lucide-react": "^0.363.0"
  },
  "devDependencies": {
    "@testing-library/react": "^14.2.0",
    "@testing-library/jest-dom": "^6.4.0",
    "@playwright/test": "^1.40.0",
    "eslint": "^8.57.0",
    "prettier": "^3.2.0",
    "husky": "^9.0.0"
  }
}
```



##  Installation

### Prérequis
- **Node.js** 18.17 ou supérieur
- **npm** ou **yarn** ou **pnpm**

### Installation des dépendances
```bash
# Cloner le repository
git clone https://github.com/BrianBrusly/YowYob-Search-Frontend.git
cd YowYob-Search-Frontend

# Installer les dépendances
npm install
# ou
yarn install
# ou
pnpm install
```

### Configuration de l'environnement
```bash
# Copier le fichier d'environnement
cp .env.example .env.local

# Éditer .env.local avec vos configurations
NEXT_PUBLIC_API_URL=http://localhost:8080
NEXT_PUBLIC_APP_URL=http://localhost:3000
NEXT_PUBLIC_GA_ID=your-google-analytics-id
```

---

##  Configuration

### Variables d'environnement

```env
# API Configuration
NEXT_PUBLIC_API_URL=http://localhost:8080
NEXT_PUBLIC_APP_URL=http://localhost:3000

# Analytics
NEXT_PUBLIC_GA_ID=G-XXXXXXXXXX

# PWA Configuration
NEXT_PUBLIC_PWA_NAME=YowYob Search
NEXT_PUBLIC_PWA_SHORT_NAME=YowYob
NEXT_PUBLIC_PWA_THEME_COLOR=#3b82f6

# Features Flags
NEXT_PUBLIC_ENABLE_PWA=true
NEXT_PUBLIC_ENABLE_ANALYTICS=false
NEXT_PUBLIC_ENABLE_DEBUG=false
```

### Configuration Next.js

```javascript
// next.config.mjs
/** @type {import('next').NextConfig} */
const nextConfig = {
  experimental: {
    appDir: true,
  },
  images: {
    domains: ['localhost', 'api.yowyob.com'],
  },
  // Configuration PWA
  ...withPWA({
    dest: 'public',
    register: true,
    skipWaiting: true,
  }),
}

export default nextConfig
```

### Configuration Tailwind CSS

```javascript
// tailwind.config.ts
import type { Config } from 'tailwindcss'

const config: Config = {
  content: [
    './src/pages/**/*.{js,ts,jsx,tsx,mdx}',
    './src/components/**/*.{js,ts,jsx,tsx,mdx}',
    './src/app/**/*.{js,ts,jsx,tsx,mdx}',
  ],
  theme: {
    extend: {
      colors: {
        primary: {
          50: '#eff6ff',
          500: '#3b82f6',
          600: '#2563eb',
          700: '#1d4ed8',
        },
      },
    },
  },
  plugins: [],
  darkMode: 'class',
}
export default config
```

---

##  Développement

### Démarrage en mode développement
```bash
npm run dev
# ou
yarn dev
# ou
pnpm dev
```

L'application sera accessible sur http://localhost:3000

### Commandes disponibles
```bash
# Développement
npm run dev          # Serveur de développement
npm run build        # Build production
npm run start        # Serveur production
npm run lint         # Linting ESLint
npm run type-check   # Vérification TypeScript

# Tests
npm run test         # Tests unitaires
npm run test:e2e     # Tests E2E avec Playwright
npm run test:coverage # Coverage des tests

# Qualité de code
npm run format       # Formatage avec Prettier
npm run analyze      # Analyse du bundle
```

### Structure d'un composant type

```typescript
// components/search/search-bar.tsx
'use client'

import { useState } from 'react'
import { useSearch } from '@/lib/hooks/use-search'
import { Input } from '@/components/ui/input'
import { SearchSuggestions } from './search-suggestions'

interface SearchBarProps {
  initialQuery?: string
  onSearch?: (query: string) => void
}

export function SearchBar({ initialQuery = '', onSearch }: SearchBarProps) {
  const [query, setQuery] = useState(initialQuery)
  const { suggestions, isLoading } = useSearch(query)

  const handleSubmit = (e: React.FormEvent) => {
    e.preventDefault()
    onSearch?.(query)
  }

  return (
    <div className="relative w-full max-w-2xl">
      <form onSubmit={handleSubmit} className="flex gap-2">
        <Input
          type="text"
          value={query}
          onChange={(e) => setQuery(e.target.value)}
          placeholder="Rechercher..."
          className="flex-1"
        />
        <button
          type="submit"
          className="px-4 py-2 bg-primary-500 text-white rounded-lg hover:bg-primary-600"
        >
          Rechercher
        </button>
      </form>
      
      <SearchSuggestions 
        suggestions={suggestions}
        isLoading={isLoading}
        onSelect={(suggestion) => setQuery(suggestion)}
      />
    </div>
  )
}
```

---

##  Tests

### Tests unitaires avec Jest
```typescript
// __tests__/components/search-bar.test.tsx
import { render, screen, fireEvent } from '@testing-library/react'
import { SearchBar } from '@/components/search/search-bar'

describe('SearchBar', () => {
  it('renders search input and button', () => {
    render(<SearchBar />)
    
    expect(screen.getByPlaceholderText('Rechercher...')).toBeInTheDocument()
    expect(screen.getByText('Rechercher')).toBeInTheDocument()
  })

  it('calls onSearch when form is submitted', () => {
    const mockOnSearch = jest.fn()
    render(<SearchBar onSearch={mockOnSearch} />)
    
    const input = screen.getByPlaceholderText('Rechercher...')
    const button = screen.getByText('Rechercher')
    
    fireEvent.change(input, { target: { value: 'test query' } })
    fireEvent.click(button)
    
    expect(mockOnSearch).toHaveBeenCalledWith('test query')
  })
})
```

### Tests E2E avec Playwright
```typescript
// e2e/search.spec.ts
import { test, expect } from '@playwright/test'

test('search functionality', async ({ page }) => {
  await page.goto('/')
  
  // Remplir la recherche
  await page.fill('input[placeholder="Rechercher..."]', 'restaurant')
  await page.click('button:has-text("Rechercher")')
  
  // Vérifier les résultats
  await expect(page.locator('.search-results')).toBeVisible()
  await expect(page.locator('.result-card').first()).toBeVisible()
})
```

### Exécution des tests
```bash
# Tests unitaires
npm run test

# Tests avec coverage
npm run test:coverage

# Tests E2E
npm run test:e2e

# Tous les tests
npm run test:all
```

---

## Build & Déploiement

### Build de production
```bash
npm run build
```

### Démarrage en production
```bash
npm start
```

### Déploiement avec Docker
```dockerfile
# Dockerfile
FROM node:18-alpine AS builder
WORKDIR /app
COPY package*.json ./
RUN npm ci --only=production

FROM node:18-alpine AS runner
WORKDIR /app
COPY --from=builder /app/node_modules ./node_modules
COPY . .
RUN npm run build

EXPOSE 3000
CMD ["npm", "start"]
```

### Déploiement sur Vercel
```bash
# Installation de Vercel CLI
npm i -g vercel

# Déploiement
vercel --prod
```

### Variables d'environnement production
```env
NEXT_PUBLIC_API_URL=https://api.yowyob.com
NEXT_PUBLIC_APP_URL=https://yowyob.com
NEXT_PUBLIC_GA_ID=G-PRODUCTION_ID
NEXT_PUBLIC_ENABLE_ANALYTICS=true
```

---

## 📱 Fonctionnalités PWA

### Configuration du manifeste
```json
// public/manifest.json
{
  "name": "YowYob Search",
  "short_name": "YowYob",
  "description": "Moteur de recherche intelligent et rapide",
  "start_url": "/",
  "display": "standalone",
  "theme_color": "#3b82f6",
  "background_color": "#ffffff",
  "icons": [
    {
      "src": "/icons/icon-72x72.png",
      "sizes": "72x72",
      "type": "image/png"
    },
    {
      "src": "/icons/icon-192x192.png",
      "sizes": "192x192",
      "type": "image/png"
    },
    {
      "src": "/icons/icon-512x512.png",
      "sizes": "512x512",
      "type": "image/png"
    }
  ]
}
```

### Service Worker personnalisé
```javascript
// public/sw.js
const CACHE_NAME = 'yowyob-v1'
const urlsToCache = [
  '/',
  '/static/js/bundle.js',
  '/static/css/main.css',
  '/manifest.json'
]

self.addEventListener('install', (event) => {
  event.waitUntil(
    caches.open(CACHE_NAME)
      .then((cache) => cache.addAll(urlsToCache))
  )
})

self.addEventListener('fetch', (event) => {
  event.respondWith(
    caches.match(event.request)
      .then((response) => {
        if (response) {
          return response
        }
        return fetch(event.request)
      }
    )
  )
})
```

### Gestion des notifications push
```typescript
// lib/pwa/push-manager.ts
export class PushManager {
  static async requestPermission(): Promise<boolean> {
    if (!('Notification' in window)) {
      return false
    }
    
    const permission = await Notification.requestPermission()
    return permission === 'granted'
  }
  
  static async subscribe(): Promise<PushSubscription | null> {
    if (!('serviceWorker' in navigator)) {
      return null
    }
    
    const registration = await navigator.serviceWorker.ready
    const subscription = await registration.pushManager.subscribe({
      userVisibleOnly: true,
      applicationServerKey: process.env.NEXT_PUBLIC_VAPID_PUBLIC_KEY
    })
    
    return subscription
  }
}
```

---

##  Design System

### Couleurs
```css
/* Thème clair */
:root {
  --primary-50: #eff6ff;
  --primary-500: #3b82f6;
  --primary-600: #2563eb;
  --gray-50: #f9fafb;
  --gray-100: #f3f4f6;
  --gray-800: #1f2937;
}

/* Thème sombre */
.dark {
  --primary-500: #60a5fa;
  --gray-50: #111827;
  --gray-100: #1f2937;
}
```

### Typographie
```css
.text-display {
  font-size: 3rem;
  font-weight: 700;
  line-height: 1.1;
}

.text-title {
  font-size: 1.5rem;
  font-weight: 600;
  line-height: 1.3;
}

.text-body {
  font-size: 1rem;
  line-height: 1.5;
}
```

### Composants réutilisables
```typescript
// components/ui/button.tsx
interface ButtonProps extends React.ButtonHTMLAttributes<HTMLButtonElement> {
  variant?: 'primary' | 'secondary' | 'danger'
  size?: 'sm' | 'md' | 'lg'
  children: React.ReactNode
}

export function Button({ 
  variant = 'primary', 
  size = 'md', 
  className = '',
  children,
  ...props 
}: ButtonProps) {
  const baseStyles = 'inline-flex items-center justify-center rounded-lg font-medium transition-colors'
  const variants = {
    primary: 'bg-primary-500 text-white hover:bg-primary-600',
    secondary: 'bg-gray-200 text-gray-900 hover:bg-gray-300',
    danger: 'bg-red-500 text-white hover:bg-red-600'
  }
  const sizes = {
    sm: 'px-3 py-1.5 text-sm',
    md: 'px-4 py-2 text-base',
    lg: 'px-6 py-3 text-lg'
  }
  
  return (
    <button
      className={`${baseStyles} ${variants[variant]} ${sizes[size]} ${className}`}
      {...props}
    >
      {children}
    </button>
  )
}
```

---

##  API Integration

### Client API configuré
```typescript
// lib/api/client.ts
import axios from 'axios'

const apiClient = axios.create({
  baseURL: process.env.NEXT_PUBLIC_API_URL,
  timeout: 10000,
})

// Intercepteur pour ajouter le token JWT
apiClient.interceptors.request.use((config) => {
  const token = localStorage.getItem('accessToken')
  if (token) {
    config.headers.Authorization = `Bearer ${token}`
  }
  return config
})

// Intercepteur pour gérer les erreurs et refresh token
apiClient.interceptors.response.use(
  (response) => response,
  async (error) => {
    if (error.response?.status === 401) {
      // Logique de refresh token
      await refreshToken()
      return apiClient.request(error.config)
    }
    return Promise.reject(error)
  }
)

export { apiClient }
```

### Hook de recherche personnalisé
```typescript
// lib/hooks/use-search.ts
import { useState, useEffect } from 'react'
import { useDebounce } from './use-debounce'
import { searchApi } from '@/lib/api/search-api'

export function useSearch(initialQuery = '') {
  const [query, setQuery] = useState(initialQuery)
  const [results, setResults] = useState<SearchResult[]>([])
  const [isLoading, setIsLoading] = useState(false)
  const [error, setError] = useState<string | null>(null)
  
  const debouncedQuery = useDebounce(query, 300)

  useEffect(() => {
    if (!debouncedQuery.trim()) {
      setResults([])
      return
    }

    const performSearch = async () => {
      setIsLoading(true)
      setError(null)
      
      try {
        const response = await searchApi.search({
          query: debouncedQuery,
          page: 0,
          size: 10
        })
        setResults(response.results)
      } catch (err) {
        setError('Erreur lors de la recherche')
        console.error('Search error:', err)
      } finally {
        setIsLoading(false)
      }
    }

    performSearch()
  }, [debouncedQuery])

  return {
    query,
    setQuery,
    results,
    isLoading,
    error
  }
}
```

### Gestion d'état avec Zustand
```typescript
// store/slices/search-slice.ts
import { create } from 'zustand'
import { searchApi } from '@/lib/api/search-api'

interface SearchState {
  query: string
  results: SearchResult[]
  isLoading: boolean
  error: string | null
  setQuery: (query: string) => void
  search: (query: string) => Promise<void>
  clearResults: () => void
}

export const useSearchStore = create<SearchState>((set, get) => ({
  query: '',
  results: [],
  isLoading: false,
  error: null,
  
  setQuery: (query) => set({ query }),
  
  search: async (query) => {
    set({ isLoading: true, error: null })
    
    try {
      const response = await searchApi.search({ query, page: 0, size: 20 })
      set({ results: response.results, isLoading: false })
    } catch (error) {
      set({ error: 'Search failed', isLoading: false })
    }
  },
  
  clearResults: () => set({ results: [], query: '' })
}))
```

---

##  Performance

### Métriques de performance cibles
- **LCP (Largest Contentful Paint)** : < 2.5s
- **FID (First Input Delay)** : < 100ms
- **CLS (Cumulative Layout Shift)** : < 0.1
- **TBT (Total Blocking Time)** : < 200ms

### Optimisations implémentées
- **Images optimisées** avec Next.js Image component
- **Code splitting** automatique avec Next.js
- **Prefetching** des routes importantes
- **Compression** gzip/brotli
- **Cache stratégique** via Service Worker

### Monitoring des performances
```typescript
// lib/utils/analytics.ts
export const trackWebVitals = (metric: any) => {
  if (process.env.NODE_ENV === 'production') {
    // Envoyer à Google Analytics
    gtag('event', 'web_vitals', {
      event_category: 'Web Vitals',
      event_label: metric.name,
      value: Math.round(metric.name === 'CLS' ? metric.value * 1000 : metric.value),
      non_interaction: true,
    })
  }
}

// Utilisation dans _app.tsx
export function reportWebVitals(metric: any) {
  trackWebVitals(metric)
}
```

---

## 🛣️ Roadmap

### Phase 1 (Complétée)
- [x] Architecture Next.js 14 avec App Router
- [x] Design System avec Tailwind CSS
- [x] Intégration API backend
- [x] Fonctionnalités PWA de base
- [x] Recherche avec suggestions

### Phase 2 ( En cours)
- [ ] Internationalisation (i18n)
- [ ] Mode hors-ligne avancé
- [ ] Analytics détaillés
- [ ] Tests E2E complets
- [ ] Performance monitoring

### Phase 3 ( Planifiée)
- [ ] Recherche vocale
- [ ] Reality augmentée
- [ ] Personalisation IA
- [ ] Social features
- [ ] Marketplace intégré

---

##  Contribution

### Processus de contribution
1. **Fork** le repository
2. **Créer une branche** : `git checkout -b feature/amazing-feature`
3. **Commit** : `git commit -m 'feat: add amazing feature'`
4. **Push** : `git push origin feature/amazing-feature`
5. **Ouvrir une Pull Request**

### Conventions de commit
```bash
feat: nouvelle fonctionnalité
fix: correction de bug
docs: documentation
style: formatage de code
refactor: refactoring de code
test: ajout/modification de tests
chore: tâches diverses
```

### Standards de code
- **ESLint** pour le linting
- **Prettier** pour le formatage
- **TypeScript** strict mode
- **Conventional Commits** pour les messages

---

##  License

MIT License - voir [LICENSE](LICENSE) pour plus de détails.

---

##  Liens utiles

- [Documentation Backend](../YowYob-Search-Backend/README.md)
- [Documentation Infrastructure](../YowYob-Search-Infrastructure/README.md)
- [Guide de déploiement](./docs/DEPLOYMENT.md)
- [Changelog](./CHANGELOG.md)

---

**Développé par l'équipe YowYob**

*Pour toute question, consultez la documentation ou ouvrez une issue sur GitHub.*
