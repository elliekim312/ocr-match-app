# OCR Match App

A cross-platform mobile app that recognizes text from images and matches it against structured data using FastAPI and PostgreSQL.

# Tech Stack
- **Mobile**: React Native (Expo), TypeScript  
- **Backend**: Python (FastAPI)  
- **Auth**: Email/Password, Google, Apple  
- **OCR**: ML Kit (on-device), Google Vision API (server-side fallback)  
- **DB**: PostgreSQL  
- **Search/Matching**: PostgreSQL FTS + `pg_trgm` + optional embeddings (`pgvector` / Qdrant)   
- **Storage**: GCS (image uploads)
- **Containers**: Docker  
- **CI/CD**: GitHub Actions  
- **Infra**:  GCP Cloud Run + Cloud SQL (Postgres) or AWS Fargate + RDS  

# Features
## 📱 App Navigation
- **Home** — personalized feed
- **Explore** — search and browse catalog entries
- **Camera** — capture and process images
- **Favorite** — saved items and quick access to user favorites
- **Profile** — user information, settings, and account management

## 🔐 Authentication
- Multi-provider login (Email, Google, Apple)
- JWT-based authentication & refresh tokens
- Profile management & basic onboarding

## 📷 Image Capture & OCR
- On-device OCR using ML Kit (React Native)
- Server-side validation using Google Vision API
- Image preprocessing (crop, brightness, noise removal)
- Privacy-first design: on-device first, upload only when needed

## 🧠 Text Processing & Matching
- Text normalization & entity extraction
- Fuzzy search via PostgreSQL FTS + Trigram similarity
- Semantic similarity via embeddings (pgvector / Qdrant)
- Confidence scoring for auto or human-assisted confirmation

## 🔍 Catalog & Metadata
- Structured catalog with searchable entries
- Fast filtering & search endpoints
- Related-item suggestions based on semantic proximity

## ⭐ User Interaction
- Ratings, reviews, favorites, and personalized statistics
- Personal activity dashboard (recent searches, favorites)
- *(Future)* Community: following, feed, comments

## 🗓️ Project Plan & Schedule
The schedule focuses on delivering an MVP in a logical build order, with learning time included.  
Estimates assume ~5–6 hours/day.

| Order | Area / Page | Scope | Estimate (days) | Notes / Acceptance Criteria |
|:--:|---|---|---:|---|
| 1 | **Frontend Sketch & Setup** | Initialize RN/Expo project, folder structure, navigation (Home / Explore / Camera / Favorite / Profile), base theme | **1–3** | App launches, tabs work, basic layout and icons ready |
| 2 | **Image Capture & OCR** | Camera permission, capture flow, on-device OCR (ML Kit), Vision API fallback, loading/error handling | **5–8** | OCR text extraction reliable; retry flow and UI tested |
| 3 | **Authentication** | Email/Password + Google/Apple login, JWT refresh, profile setup, onboarding | **3–5** | Full login/logout works; tokens refresh; onboarding complete |
| 4 | **Text Processing & Matching** | Normalize text, extract entities, implement FTS + Trigram search, optional embeddings | **6–10** | Matching returns top 2–3 candidates; confidence scoring visible |
| 5 | **Catalog & Metadata** | DB schema, initial seed data, metadata fields, Alembic migrations, indexing | **3–7** | Catalog entries searchable and linked to matching results |
| 6 | **Home Feed** | Sections: Recommended for You, Bestsellers, Recently Searched, Trending | **3–5** | Feed loads dynamically; empty-state and error handling in place |
| 7 | **Explore / Search Page** | Search by text, category tags, filters, sort options | **3–5** | Debounced search; results render smoothly; no crashes on empty |
| 8 | **Item Listing & Details** | List view with infinite scroll; item details (image, meta, similar items) | **3-5** | Item details show correct info; navigation from Explore works |
| 9 | **Favorite Page** | List, sort, remove, sync favorites between sessions | **2-4** | Favorites persist after relaunch; feedback toast shown |
| 10 | **Profile Page** | Ratings, reviews, favorites summary, user activity & preference overview | **3–5** | Displays personal stats or summary text; editable profile info |
| 11 | **Frontend Design Update** | Apply refined styling, spacing, and responsive layout | **3–5** | Unified visual theme; consistent spacing and color usage |
| 12 | **Monetization & Ads Integration** | Implement AdMob banner (Home/Explore) and native ad in feed | **3–5** | Ads load conditionally; can toggle via config (AD_ENABLED=false) |
| 13 | **Backend Glue & APIs** | Define REST endpoints, middleware, pagination, filtering, rate limiting | **3–5** | API passes Postman tests; OpenAPI auto-doc generated |
| 14 | **CI/CD & Monitoring** | GitHub Actions pipeline, Sentry error tracking, OpenTelemetry tracing | **1–2** | Auto build/test/deploy; monitoring connected |

> **Total (MVP mid-range):** ~ **35–60 workdays**  
> Focus order: Camera/OCR → Matching → Catalog/Search → Auth → Feed/Favorites → Profile

## 💰 Monetization Plan

- **Phase 1 – Free Tier (Launch)**  
  - All features free, no paywall  
  - Include **AdMob banner** on Home/Explore and one **native ad** in the feed  
  - Ads can be toggled via config variable (`AD_ENABLED`)

- **Phase 2 – Ad-Free Tier (Later Update)**  
  - Remove ads, unlock faster text-matching/filtering  
  - In-app purchase: **$1.99–$2.99/month**

- **Phase 3 – Pro Tier (Future)**  
  - Advanced features: AI recommendations, personalized analytics, detailed stats  
  - Subscription **$4.99/month** or one-time purchase

## 🔒 Repository Visibility
This project’s implementation is currently hosted in a **private repository** for internal development and deployment.  
This public README is shared for portfolio purposes only.

## Getting Started
```bash
# backend
cd backend
uvicorn app.main:app --reload

# frontend
cd frontend
npm install
npm start
