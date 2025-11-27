#  YowYob Search PWA - Frontend

##  Vue d'ensemble Frontend

**YowYob Search Frontend** est une Progressive Web App (PWA) moderne construite avec Next.js 14, offrant une expérience utilisateur performante et réactive.

###  Objectifs architecturaux
-  **Performance optimale** avec Server Components et Streaming SSR
-  **Expérience native** via PWA (installation, offline, push)
-  **Maintenabilité** avec architecture modulaire et TypeScript
-  **Scalabilité** avec state management léger (Zustand)
-  **Accessibilité** conforme WCAG 2.1 AA

---

## 📁 Structure Complète du Frontend

```
yowyob-search-frontend/
├── 📁 public/                          # Assets statiques
│   ├── 📄 manifest.json               # Configuration PWA
│   ├── 📄 sw.js                       # Service Worker
│   ├── 📄 offline.html                # Page hors ligne
│   └── 📁 icons/                      # Icônes PWA (72x72 à 512x512)
│
├── 📁 src/
│   ├── 📁 app/                        # App Router Next.js 14+
│   │   ├── 📄 layout.tsx              # Layout racine avec providers
│   │   ├── 📄 page.tsx                # Page d'accueil
│   │   ├── 📄 globals.css             # Styles Tailwind + custom
│   │   ├── 📄 loading.tsx             # Composant loading global
│   │   ├── 📄 error.tsx               # Error boundary global
│   │   ├── 📄 not-found.tsx           # Page 404
│   │   │
│   │   ├── 📁 search/                 # Route /search
│   │   │   ├── 📄 page.tsx            # Page résultats recherche
│   │   │   └── 📄 loading.tsx         # Skeleton search
│   │   │
│   │   ├── 📁 auth/                   # Routes authentification
│   │   │   ├── 📁 login/
│   │   │   │   └── 📄 page.tsx        # Page connexion
│   │   │   ├── 📁 register/
│   │   │   │   └── 📄 page.tsx        # Page inscription
│   │   │   └── 📁 forgot-password/
│   │   │       └── 📄 page.tsx        # Page mot de passe oublié
│   │   │
│   │   ├── 📁 profile/                # Profil utilisateur
│   │   │   ├── 📄 page.tsx            # Page profil
│   │   │   └── 📁 history/
│   │   │       └── 📄 page.tsx        # Historique recherches
│   │   │
│   │   └── 📁 api/                    # API Routes (optionnel)
│   │       └── 📁 health/
│   │           └── 📄 route.ts        # Endpoint santé
│   │
│   ├── 📁 components/                 # Composants réutilisables
│   │   ├── 📁 layout/                 # Composants structurels
│   │   │   ├── 📄 Header.tsx          # En-tête avec navigation
│   │   │   ├── 📄 Footer.tsx          # Pied de page
│   │   │   ├── 📄 Sidebar.tsx         # Barre latérale filtres
│   │   │   └── 📄 MobileMenu.tsx      # Menu mobile
│   │   │
│   │   ├── 📁 search/                 # Composants domaine recherche
│   │   │   ├── 📄 SearchBar.tsx       # Barre recherche avec debounce
│   │   │   ├── 📄 SearchSuggestions.tsx # Suggestions autocomplete
│   │   │   ├── 📄 SearchFilters.tsx   # Filtres (date, type, langue)
│   │   │   ├── 📄 ResultsList.tsx     # Liste résultats paginée
│   │   │   ├── 📄 ResultCard.tsx      # Carte résultat individuel
│   │   │   ├── 📄 ResultSkeleton.tsx  # Placeholder loading
│   │   │   ├── 📄 Pagination.tsx      # Navigation pages
│   │   │   ├── 📄 NoResults.tsx       État aucun résultat
│   │   │   └── 📄 TrendingSearches.tsx # Tendances recherches
│   │   │
│   │   ├── 📁 map/                    # Composants cartographie
│   │   │   ├── 📄 MapComponent.tsx    # Carte Leaflet principale
│   │   │   ├── 📄 MapMarker.tsx       # Marqueurs géolocalisés
│   │   │   ├── 📄 MapPopup.tsx        # Popups informations
│   │   │   └── 📄 MapControls.tsx     # Contrôles zoom/layers
│   │   │
│   │   ├── 📁 auth/                   # Composants authentification
│   │   │   ├── 📄 LoginForm.tsx       # Formulaire connexion
│   │   │   ├── 📄 RegisterForm.tsx    # Formulaire inscription
│   │   │   ├── 📄 ForgotPasswordForm.tsx
│   │   │   ├── 📄 ResetPasswordForm.tsx
│   │   │   └── 📄 ProtectedRoute.tsx  # HOC protection routes
│   │   │
│   │   ├── 📁 common/                 # Composants UI réutilisables
│   │   │   ├── 📄 Button.tsx          # Bouton avec variants
│   │   │   ├── 📄 Input.tsx           # Input contrôlé
│   │   │   ├── 📄 Card.tsx            # Container card
│   │   │   ├── 📄 Modal.tsx           # Modal/dialog
│   │   │   ├── 📄 Spinner.tsx         # Loader circulaire
│   │   │   ├── 📄 Alert.tsx           # Messages alerte
│   │   │   ├── 📄 Badge.tsx           # Labels/tags
│   │   │   ├── 📄 Avatar.tsx          # Avatar utilisateur
│   │   │   ├── 📄 Tooltip.tsx         # Infobulles
│   │   │   ├── 📄 Dropdown.tsx        # Menu déroulant
│   │   │   └── 📄 Tabs.tsx            # Navigation par onglets
│   │   │
│   │   └── 📁 pwa/                    # Composants PWA
│   │       ├── 📄 InstallPrompt.tsx   # Prompt installation A2HS
│   │       ├── 📄 UpdateNotification.tsx # Notification MAJ
│   │       ├── 📄 OfflineIndicator.tsx # Indicateur connexion
│   │       └── 📄 PushNotificationToggle.tsx # Toggle notifications
│   │
│   ├── 📁 lib/                        # Utilitaires et configuration
│   │   ├── 📁 api/                    # Clients API
│   │   │   ├── 📄 client.ts           # Configuration Axios + intercepteurs
│   │   │   ├── 📄 endpoints.ts        # URLs des endpoints backend
│   │   │   ├── 📄 searchApi.ts        # Appels Search Service
│   │   │   ├── 📄 authApi.ts          # Appels User Service
│   │   │   ├── 📄 geoApi.ts           # Appels Geo Service
│   │   │   └── 📄 notificationApi.ts  # Appels Notification Service
│   │   │
│   │   ├── 📁 hooks/                  # Custom React Hooks
│   │   │   ├── 📄 useSearch.ts        # Hook recherche avec debounce
│   │   │   ├── 📄 useAuth.ts          # Hook authentification
│   │   │   ├── 📄 useGeolocation.ts   # Hook géolocalisation navigateur
│   │   │   ├── 📄 useLocalStorage.ts  # Hook localStorage typé
│   │   │   ├── 📄 useDebounce.ts      # Hook debounce générique
│   │   │   ├── 📄 useInfiniteScroll.ts # Scroll infini
│   │   │   ├── 📄 useOnlineStatus.ts  # Détection online/offline
│   │   │   └── 📄 usePushNotifications.ts # Gestion notifications push
│   │   │
│   │   ├── 📁 utils/                  # Fonctions utilitaires
│   │   │   ├── 📄 formatters.ts       # Format dates, nombres, textes
│   │   │   ├── 📄 validators.ts       # Validation formulaires
│   │   │   ├── 📄 storage.ts          # Wrappers localStorage/sessionStorage
│   │   │   ├── 📄 seo.ts              # Génération meta tags dynamiques
│   │   │   ├── 📄 analytics.ts        # Wrapper Google Analytics
│   │   │   └── 📄 errorHandlers.ts    # Gestion centralisée erreurs
│   │   │
│   │   ├── 📁 constants/              # Constantes applicatives
│   │   │   ├── 📄 routes.ts           # URLs des routes internes
│   │   │   ├── 📄 config.ts           # Configuration globale
│   │   │   └── 📄 searchTypes.ts      # Types de recherche disponibles
│   │   │
│   │   └── 📁 pwa/                    # Logique PWA
│   │       ├── 📄 serviceWorker.ts    # Enregistrement Service Worker
│   │       ├── 📄 pushManager.ts      # Gestion notifications push
│   │       └── 📄 installPrompt.ts    # Logique installation A2HS
│   │
│   ├── 📁 store/                      # State Management (Zustand)
│   │   ├── 📄 index.ts                # Store racine combiné
│   │   ├── 📁 slices/                 # Slices de state
│   │   │   ├── 📄 searchSlice.ts      # State recherche (query, results)
│   │   │   ├── 📄 authSlice.ts        # State authentification (user, token)
│   │   │   ├── 📄 uiSlice.ts          # State UI (theme, sidebar, modals)
│   │   │   └── 📄 notificationSlice.ts # State notifications
│   │   │
│   │   └── 📁 middleware/             # Middlewares store
│   │       └── 📄 logger.ts           # Logging des actions
│   │
│   ├── 📁 types/                      # Types TypeScript
│   │   ├── 📄 api.ts                  # Types réponses API
│   │   ├── 📄 search.ts               # Types recherche
│   │   ├── 📄 user.ts                 # Types utilisateur
│   │   ├── 📄 geo.ts                  # Types géolocalisation
│   │   └── 📄 common.ts               # Types communs
│   │
│   └── 📁 styles/                     # Styles additionnels
│       ├── 📄 globals.css             # Styles globaux Tailwind + custom
│       ├── 📁 themes/                 # Système de thèmes
│       │   ├── 📄 light.css           # Variables thème clair
│       │   └── 📄 dark.css            # Variables thème sombre
│       └── 📄 animations.css          # Animations CSS customisées
│
├── 📄 middleware.ts                   # Middleware Next.js (auth, i18n)
├── 📄 next.config.mjs                 # Configuration Next.js + PWA
├── 📄 tailwind.config.ts              # Configuration Tailwind CSS
├── 📄 tsconfig.json                   # Configuration TypeScript
├── 📄 package.json
└── 📄 README.md
```

---

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
