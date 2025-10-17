# 🚀 AI-Powered MVP Development Guide
## Агрегатор недвижимости BN-24

> **Цель:** Создать полнофункциональный MVP за 7-10 дней с максимальным использованием ИИ для генерации кода, тестирования и деплоя.

---

## 📋 Оглавление

1. [Обзор проекта](#обзор-проекта)
2. [Техническая архитектура](#техническая-архитектура)
3. [Структура проекта](#структура-проекта)
4. [AI Prompts по этапам](#ai-prompts-по-этапам)
5. [AI Workflow Example](#ai-workflow-example)
6. [Контроль качества](#контроль-качества)
7. [Деплой и мониторинг](#деплой-и-мониторинг)

---

## 🎯 Обзор проекта

### Бизнес-цель
Создание агрегатора недвижимости с моделью "оплата за результат", устраняющего посредников и снижающего стоимость сделок на 60-70%.

### Ключевые особенности
- 30,000+ объектов недвижимости
- Прямые сделки собственник-покупатель
- Верификация объектов и собственников
- Оплата только при успешной продаже
- Полное юридическое сопровождение

### Технические требования
- **Производительность:** Core Web Vitals > 90, TTI < 3s
- **SEO:** SSR, динамические мета-теги, sitemap
- **Масштабируемость:** поддержка 30k+ объектов
- **Интеграция:** Bitrix24 CRM, Яндекс.Карты
- **Безопасность:** JWT, HTTPS, валидация данных

---

## 🏗 Техническая архитектура

### Frontend Stack
```yaml
Framework: Nuxt 3 (SSR + SPA)
Language: TypeScript
Styling: Tailwind CSS + SCSS
State: Pinia
API: $fetch (нативный)
Maps: Яндекс.Карты API
PWA: @vite-pwa/nuxt
Testing: Vitest + Testing Library
```

### Backend Stack
```yaml
Framework: Nest.js
Database: Redis (кэш) + PostgreSQL (основная БД)
API: REST + GraphQL (опционально)
Auth: JWT + OAuth2
Integration: Bitrix24 REST API
Container: Docker + Docker Compose
```

### Infrastructure
```yaml
Hosting: VPS (DigitalOcean/AWS)
CDN: CloudFlare
CI/CD: GitHub Actions
Monitoring: Sentry + UptimeRobot
Backup: AWS S3 + автоматические дампы
```

---

## 📁 Структура проекта

```
bn24-mvp/
├── apps/
│   ├── frontend/          # Nuxt 3 приложение
│   ├── bff/              # Nest.js BFF
│   └── admin/            # Админ-панель (опционально)
├── packages/
│   ├── shared/           # Общие типы и утилиты
│   ├── ui/              # UI компоненты
│   └── config/          # Конфигурации
├── docs/                # Документация
├── scripts/             # Скрипты автоматизации
├── docker-compose.yml   # Локальная разработка
├── .github/
│   └── workflows/       # CI/CD пайплайны
└── README.md
```

---

## 🤖 AI Prompts по этапам

### Этап 1: Инициализация проекта

#### 1.1 Создание структуры monorepo

**Промпт:**
```
Создай monorepo структуру для MVP агрегатора недвижимости:

1. apps/frontend/ - Nuxt 3 с TypeScript, Tailwind, Pinia
2. apps/bff/ - Nest.js с Redis, JWT, OpenAPI
3. packages/shared/ - общие типы и утилиты
4. packages/ui/ - переиспользуемые UI компоненты

Включи:
- package.json с workspaces
- TypeScript конфигурации
- ESLint + Prettier настройки
- Docker Compose для локальной разработки
- .env.example файлы
- .gitignore для всех типов файлов

Структура должна поддерживать:
- Hot reload в разработке
- TypeScript strict mode
- Автоматическое форматирование кода
- Линтинг на pre-commit
```

#### 1.2 Настройка CI/CD

**Промпт:**
```
Создай GitHub Actions workflow для monorepo:

1. ci.yml - линт, тест, build для всех приложений
2. deploy-staging.yml - деплой на staging
3. deploy-production.yml - деплой на production
4. rollback.yml - откат версии
5. backup.yml - резервное копирование БД

Особенности:
- Кэширование node_modules
- Параллельный запуск тестов
- Условный деплой только измененных приложений
- Автоматический rollback при ошибках
- Уведомления в Slack/Telegram
- Секреты через GitHub Secrets

Используй Docker для сборки и деплоя.
```

### Этап 2: Frontend разработка

#### 2.1 Настройка Nuxt 3

**Промпт:**
```
Создай Nuxt 3 приложение с полной конфигурацией:

Технологии:
- Nuxt 3 + TypeScript (strict mode)
- Tailwind CSS + SCSS модули
- Pinia для состояния
- @nuxtjs/i18n для интернационализации
- @pinia/nuxt для SSR состояния
- @vite-pwa/nuxt для PWA

Страницы:
- / - главная с поиском и превью объектов
- /catalog - каталог с фильтрами и картой
- /object/[id] - детальная страница объекта
- /login, /register - авторизация
- /profile - личный кабинет
- /add-property - добавление объекта

Компоненты:
- PropertyCard - карточка объекта
- PropertyFilter - фильтры каталога
- PropertyGallery - галерея изображений
- MapComponent - интерактивная карта
- SearchForm - форма поиска

Особенности:
- SSR для всех страниц
- SEO оптимизация (meta, sitemap, robots)
- Lazy loading изображений
- Виртуальный скролл для каталога
- Responsive design (mobile-first)
- Accessibility (ARIA, keyboard navigation)
- Error boundaries
- Loading states

Создай полную структуру с примерами компонентов.
```

#### 2.2 Генерация UI компонентов

**Промпт:**
```
Создай библиотеку UI компонентов на основе дизайн-системы:

Компоненты:
- Button (primary, secondary, outline, ghost)
- Input (text, email, password, search)
- Select (single, multi, searchable)
- Checkbox, Radio, Switch
- Modal, Drawer, Toast
- Card, Badge, Avatar
- Pagination, Skeleton
- Map (с интеграцией Яндекс.Карт)

Требования:
- TypeScript интерфейсы для всех пропсов
- Tailwind CSS классы
- Dark mode поддержка
- Responsive breakpoints
- Accessibility атрибуты
- Storybook stories (опционально)
- Unit тесты для каждого компонента

Создай также:
- Цветовую палитру в Tailwind config
- Типографическую шкалу
- Spacing систему
- Анимации и transitions
```

#### 2.3 Интеграция с API

**Промпт:**
```
Создай API слой для работы с BFF:

Сервисы:
- PropertyService - работа с объектами
- AuthService - авторизация
- UserService - пользователи
- SearchService - поиск и фильтрация
- MapService - работа с картами

Особенности:
- TypeScript типы для всех API ответов
- Автоматическая обработка ошибок
- Retry логика для failed запросов
- Кэширование в Pinia store
- Loading состояния
- Offline поддержка (Service Worker)

Методы:
- getProperties(filters, pagination)
- getPropertyById(id)
- searchProperties(query, location)
- addToFavorites(id)
- createLead(propertyId, contactData)
- uploadImages(files)

Используй $fetch с interceptors для:
- Добавления JWT токена
- Обработки 401 ошибок
- Логирования запросов
- Показ toast уведомлений
```

### Этап 3: Backend разработка

#### 3.1 Настройка Nest.js BFF

**Промпт:**
```
Создай Nest.js BFF с полной архитектурой:

Модули:
- AuthModule - JWT + OAuth2
- PropertyModule - CRUD объектов
- UserModule - управление пользователями
- SearchModule - поиск и фильтрация
- BitrixModule - интеграция с CRM
- CacheModule - Redis кэширование

API Endpoints:
- GET /api/properties - список объектов
- GET /api/properties/:id - детальная информация
- POST /api/properties - создание объекта
- PUT /api/properties/:id - обновление
- DELETE /api/properties/:id - удаление
- GET /api/search - поиск объектов
- POST /api/auth/login - авторизация
- POST /api/auth/register - регистрация
- GET /api/user/profile - профиль пользователя

Особенности:
- OpenAPI документация (Swagger)
- Валидация через class-validator
- Глобальная обработка ошибок
- Логирование через Winston
- Rate limiting
- CORS настройки
- Health check endpoint
- Metrics endpoint

Создай также:
- DTO классы для всех запросов/ответов
- Guards для авторизации
- Interceptors для логирования
- Pipes для валидации
- Exception filters
```

#### 3.2 Интеграция с Bitrix24

**Промпт:**
```
Создай модуль интеграции с Bitrix24 CRM:

Функциональность:
- Авторизация через OAuth2
- Синхронизация объектов недвижимости
- Создание лидов и сделок
- Управление контактами
- Отправка уведомлений

Методы:
- authenticate() - получение токена
- syncProperties() - синхронизация объектов
- createLead(propertyId, contactData)
- createDeal(leadId, propertyId)
- updateContact(contactId, data)
- sendNotification(userId, message)

Особенности:
- Retry логика для failed запросов
- Кэширование токенов в Redis
- Batch операции для массовых обновлений
- Логирование всех API вызовов
- Обработка rate limits
- Webhook обработчики

Создай также:
- Конфигурацию для разных окружений
- Типы для Bitrix API ответов
- Утилиты для преобразования данных
- Тесты для всех методов
```

#### 3.3 Настройка базы данных

**Промпт:**
```
Создай схему базы данных для агрегатора недвижимости:

Таблицы:
- users - пользователи системы
- properties - объекты недвижимости
- property_images - изображения объектов
- property_features - характеристики
- favorites - избранные объекты
- leads - лиды/заявки
- deals - сделки
- search_history - история поиска
- user_sessions - сессии пользователей

Особенности:
- PostgreSQL с индексами для поиска
- Redis для кэширования
- Миграции через TypeORM
- Seeds для тестовых данных
- Backup стратегия
- Connection pooling

Создай также:
- Entity классы для TypeORM
- Repository паттерн
- Query builder утилиты
- Database health checks
- Performance мониторинг
```

### Этап 4: Интеграция и тестирование

#### 4.1 E2E тестирование

**Промпт:**
```
Создай E2E тесты с Playwright:

Сценарии:
1. Регистрация нового пользователя
2. Поиск объектов недвижимости
3. Просмотр детальной страницы объекта
4. Добавление в избранное
5. Создание заявки на объект
6. Авторизация существующего пользователя
7. Управление профилем
8. Добавление нового объекта

Особенности:
- Тесты для desktop и mobile
- Скриншоты при ошибках
- Видео записи тестов
- Параллельный запуск
- CI интеграция
- Page Object Model

Создай также:
- Fixtures для тестовых данных
- Утилиты для авторизации
- Хелперы для работы с формами
- Конфигурацию для разных окружений
```

#### 4.2 Unit и Integration тесты

**Промпт:**
```
Создай полное покрытие тестами:

Frontend (Vitest + Testing Library):
- Компоненты (рендеринг, взаимодействие)
- Composables (логика, состояние)
- API сервисы (запросы, обработка ошибок)
- Utils функции
- Store actions и mutations

Backend (Jest + Supertest):
- Controllers (HTTP endpoints)
- Services (бизнес логика)
- Repositories (работа с БД)
- Utils функции
- Guards и Interceptors

Особенности:
- Mock внешних зависимостей
- Test fixtures и factories
- Coverage отчеты
- Snapshot тестирование
- Performance тесты

Цель: >80% покрытие кода
```

### Этап 5: SEO и производительность

#### 5.1 SEO оптимизация

**Промпт:**
```
Настрой SEO для агрегатора недвижимости:

Мета-теги:
- Динамические title и description
- Open Graph для соцсетей
- Twitter Cards
- Canonical URLs
- Hreflang для мультиязычности

Структурированные данные:
- Schema.org для объектов недвижимости
- Breadcrumbs
- LocalBusiness
- FAQ schema

Техническое SEO:
- Sitemap.xml с приоритетами
- Robots.txt
- 404 страница
- Redirects для старых URL
- Core Web Vitals оптимизация

Создай также:
- SEO компонент для мета-тегов
- Утилиты для генерации structured data
- Sitemap генератор
- SEO аудит скрипт
```

#### 5.2 Оптимизация производительности

**Промпт:**
```
Оптимизируй производительность приложения:

Frontend:
- Code splitting по роутам
- Lazy loading компонентов
- Image optimization (WebP, lazy loading)
- Bundle analysis и tree shaking
- Service Worker для кэширования
- Preloading критических ресурсов

Backend:
- Redis кэширование запросов
- Database query optimization
- Connection pooling
- Compression middleware
- Rate limiting
- CDN для статических файлов

Метрики:
- Lighthouse score >90
- First Contentful Paint <1.5s
- Largest Contentful Paint <2.5s
- Cumulative Layout Shift <0.1
- Time to Interactive <3s

Создай также:
- Performance monitoring
- Bundle analyzer
- Lighthouse CI
- Performance budgets
```

### Этап 6: Деплой и мониторинг

#### 6.1 Docker контейнеризация

**Промпт:**
```
Создай Docker конфигурацию для production:

Dockerfile для каждого сервиса:
- Multi-stage builds
- Alpine Linux base images
- Non-root пользователи
- Health checks
- Security scanning

Docker Compose:
- Frontend (Nuxt)
- Backend (Nest.js)
- Database (PostgreSQL)
- Cache (Redis)
- Reverse Proxy (Nginx)
- Monitoring (Prometheus + Grafana)

Особенности:
- Environment variables
- Volume mounts для данных
- Network isolation
- Resource limits
- Restart policies
- Logging configuration

Создай также:
- .dockerignore файлы
- Docker health check скрипты
- Production docker-compose.yml
- Development override файл
```

#### 6.2 Мониторинг и алерты

**Промпт:**
```
Настрой мониторинг и алертинг:

Метрики:
- Application performance (APM)
- Infrastructure metrics (CPU, RAM, Disk)
- Database performance
- API response times
- Error rates и exceptions
- User behavior analytics

Инструменты:
- Sentry для error tracking
- UptimeRobot для availability
- Prometheus + Grafana для метрик
- Log aggregation (ELK stack)
- Real User Monitoring (RUM)

Алерты:
- High error rate (>5%)
- Slow response times (>2s)
- Database connection issues
- Disk space warnings
- Memory usage alerts
- SSL certificate expiration

Создай также:
- Dashboard для мониторинга
- Alerting rules
- Escalation policies
- Incident response playbook
```

---

## 🚀 AI Workflow Example

### Полный оркестратор генерации MVP за 7-10 дней

#### День 1: Инициализация и настройка

**Утром (2-3 часа):**
```bash
# Шаг 1: Создание структуры проекта
Промпт: "Создай monorepo структуру для MVP агрегатора недвижимости с apps/frontend, apps/bff, packages/shared, полной конфигурацией TypeScript, ESLint, Prettier, Docker Compose"

# Шаг 2: Настройка CI/CD
Промпт: "Создай GitHub Actions workflow с ci.yml, deploy-staging.yml, deploy-production.yml, rollback.yml, backup.yml для monorepo с Docker"

# Шаг 3: Базовая конфигурация
Промпт: "Настрой package.json с workspaces, TypeScript конфигурации, .env.example файлы, .gitignore для всех типов файлов"
```

**Днем (3-4 часа):**
```bash
# Шаг 4: Frontend инициализация
Промпт: "Создай Nuxt 3 приложение с TypeScript, Tailwind, Pinia, полной структурой страниц /, /catalog, /object/[id], /login, /register, /profile"

# Шаг 5: Backend инициализация
Промпт: "Создай Nest.js BFF с Redis, JWT, OpenAPI, модулями Auth, Property, User, Search, Bitrix, полными API endpoints"
```

**Вечером (1-2 часа):**
```bash
# Шаг 6: Проверка и тестирование
Промпт: "Создай базовые тесты для frontend (Vitest) и backend (Jest), проверь что все сервисы запускаются через docker-compose up"
```

#### День 2: UI компоненты и API интеграция

**Утром (3-4 часа):**
```bash
# Шаг 7: UI библиотека
Промпт: "Создай библиотеку UI компонентов (Button, Input, Select, Modal, Card, Map) с TypeScript, Tailwind, accessibility, responsive design"

# Шаг 8: API слой
Промпт: "Создай API сервисы (PropertyService, AuthService, UserService, SearchService, MapService) с TypeScript типами, error handling, caching"
```

**Днем (3-4 часа):**
```bash
# Шаг 9: Интеграция Bitrix24
Промпт: "Создай модуль интеграции с Bitrix24 CRM с OAuth2, синхронизацией объектов, созданием лидов и сделок, retry логикой"

# Шаг 10: База данных
Промпт: "Создай схему PostgreSQL с таблицами users, properties, property_images, leads, deals, миграциями, seeds для тестовых данных"
```

#### День 3: Основной функционал

**Утром (4-5 часов):**
```bash
# Шаг 11: Главная страница
Промпт: "Реализуй главную страницу с HeroSection, QuickSearch, FeaturedProperties, AdvantagesSection, HowItWorks, полной SEO оптимизацией"

# Шаг 12: Каталог объектов
Промпт: "Создай каталог с PropertyFilter, PropertyGrid, MapComponent, виртуальным скроллом, URL sync состояния, поиском по карте"
```

**Днем (3-4 часа):**
```bash
# Шаг 13: Детальные страницы
Промпт: "Реализуй детальную страницу объекта с PropertyGallery, PropertyDetails, SellerInfo, ContactForm, SimilarProperties, интерактивной картой"

# Шаг 14: Авторизация
Промпт: "Создай систему авторизации с JWT, OAuth2, защищенными роутами, личным кабинетом, управлением профилем"
```

#### День 4: Поиск и фильтрация

**Утром (3-4 часа):**
```bash
# Шаг 15: Поисковая система
Промпт: "Реализуй полнотекстовый поиск с фильтрами по цене, площади, комнатам, району, сортировкой, кэшированием в Redis"

# Шаг 16: Карты и геолокация
Промпт: "Интегрируй Яндекс.Карты с поиском по карте, кластеризацией объектов, геолокацией пользователя, маршрутами"
```

**Днем (3-4 часа):**
```bash
# Шаг 17: Избранное и история
Промпт: "Добавь функционал избранных объектов, историю просмотров, рекомендации, уведомления о новых объектах"

# Шаг 18: Формы и валидация
Промпт: "Создай формы добавления объекта, контактные формы, валидацию данных, обработку файлов, preview изображений"
```

#### День 5: Тестирование и оптимизация

**Утром (4-5 часов):**
```bash
# Шаг 19: E2E тесты
Промпт: "Создай E2E тесты с Playwright для всех основных сценариев: регистрация, поиск, просмотр объекта, создание заявки"

# Шаг 20: Unit тесты
Промпт: "Создай unit тесты для всех компонентов и сервисов с покрытием >80%, mock внешних зависимостей"
```

**Днем (3-4 часа):**
```bash
# Шаг 21: SEO оптимизация
Промпт: "Настрой SEO с динамическими мета-тегами, structured data, sitemap.xml, robots.txt, Core Web Vitals оптимизацией"

# Шаг 22: Производительность
Промпт: "Оптимизируй производительность: code splitting, lazy loading, image optimization, Redis кэширование, bundle analysis"
```

#### День 6: Интеграция и деплой

**Утром (3-4 часа):**
```bash
# Шаг 23: Полная интеграция
Промпт: "Интегрируй все компоненты, настрой полный flow от поиска до создания сделки в Bitrix24, добавь error handling"

# Шаг 24: Docker контейнеризация
Промпт: "Создай production Docker конфигурацию с multi-stage builds, security scanning, health checks, docker-compose"
```

**Днем (3-4 часа):**
```bash
# Шаг 25: Staging деплой
Промпт: "Настрой деплой на staging сервер, проверь все функции, настрой мониторинг и алерты"

# Шаг 26: Production деплой
Промпт: "Выполни production деплой с blue-green стратегией, настрой backup и rollback процедуры"
```

#### День 7: Финальная проверка и запуск

**Утром (2-3 часа):**
```bash
# Шаг 27: Финальное тестирование
Промпт: "Проведи полное тестирование всех функций, проверь производительность, SEO, безопасность, мобильную версию"

# Шаг 28: Документация
Промпт: "Создай README с инструкциями по запуску, API документацию, deployment guide, troubleshooting"
```

**Днем (2-3 часа):**
```bash
# Шаг 29: Мониторинг и алерты
Промпт: "Настрой Sentry, UptimeRobot, Prometheus, создай dashboard для мониторинга, настрой алерты"

# Шаг 30: Запуск MVP
Промпт: "Выполни финальный запуск MVP, проверь все метрики, подготовь отчет для инвесторов"
```

---

## ✅ Контроль качества

### Метрики качества кода
- **Test Coverage:** >80%
- **TypeScript:** strict mode, zero any types
- **ESLint:** zero errors, warnings <10
- **Performance:** Lighthouse score >90
- **Accessibility:** WCAG 2.1 AA compliance
- **Security:** OWASP Top 10 compliance

### Процесс проверки
1. **Pre-commit hooks:** линт, форматирование, тесты
2. **CI pipeline:** полное тестирование, сборка, деплой
3. **Code review:** автоматические проверки + AI review
4. **Performance testing:** Lighthouse CI, load testing
5. **Security scanning:** dependency audit, SAST

---

## 🚀 Деплой и мониторинг

### Staging Environment
- Автоматический деплой из develop ветки
- Тестовые данные и mock сервисы
- Полное тестирование перед production

### Production Environment
- Blue-green deployment
- Автоматический rollback при ошибках
- Zero-downtime updates
- Database migrations с rollback

### Мониторинг
- **Uptime:** 99.9% SLA
- **Performance:** <2s response time
- **Errors:** <1% error rate
- **Security:** real-time threat detection

---

## 📞 Поддержка и развитие

### После запуска MVP
1. **Неделя 1-2:** Мониторинг, исправление критических багов
2. **Неделя 3-4:** Оптимизация производительности, A/B тестирование
3. **Месяц 2:** Добавление новых функций на основе обратной связи
4. **Месяц 3+:** Масштабирование, новые интеграции

### Ключевые метрики для отслеживания
- Конверсия посетителей в лиды
- Время от заявки до сделки
- Удовлетворенность пользователей
- Техническая производительность
- ROI от рекламных кампаний

---

*Этот документ является живым руководством и должен обновляться по мере развития проекта и появления новых AI инструментов.*