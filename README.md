# OCR Discovery App

A cross-platform mobile application that bridges the physical and digital worlds. It leverages on-device OCR and LLMs to recognize text from images, retrieve metadata via external APIs, and match it against a structured database using FastAPI and PostgreSQL.

# Tech Stack
- **Mobile**: React Native (Expo), TypeScript  
- **Backend**: Python (FastAPI)  
- **Auth**: Supabase Auth (Email/Password, Google, Apple)
- **DB**: PostgreSQL
- **OCR**:
  - Client-side: React Native Document Scanner, ML Kit
  - Server-side: OpenAI API (LLM), Google Search API
- **Infra**: Supabase (database, auth, storage)
- **CI/CD**: GitHub

# Features
## 📱 App Navigation
- **Home**: Personalized feed featuring "Today's Pick for you," "Trending Now," "New Arrivals," and onboarding quizzes.
- **Scan**: Camera interface for capturing product and processing text.
- **Collection**: Digital archive of user-saved items and favorites.
- **Profile**: User activity dashboard, settings, and account management.

## 🔐 Authentication
- Multi-provider login support (Email, Google, Apple).
- Secure JWT-based session management with refresh tokens.
- Streamlined profile management and onboarding flow.

## 📷 Image Capture
1. Capture: On-device OCR using ML Kit for instant text extraction.
2. Validation:
 - Existing Items: Instant match with server-side validation. 
 - New Discoveries: If the item is not in the DB, the Discovery Pipeline triggers:
  - Search: Text via Google Search API
  - LLM: Combines OCR raw text with search results to generate a structured JSON profile (Name, Attributes, Description).
  - User Verification: Presents the AI-generated data to the user for editing and final confirmation.
- Privacy-first design: on-device first, upload only when needed

## 🧠 Text Processing & Matching
- Normalization: Text cleaning and entity extraction.
- Hybrid Search: Combines Fuzzy Search (PostgreSQL Trigram) for typos with Semantic Search (Vector Embeddings) for context.
- Scoring: Confidence scoring system to determine if an item requires human review.

## ⭐ User Interaction
- Ratings, reviews, favorites, and personalized consumption statistics
- Activity dashboard tracking recent searches and favorites
- *(Future)* Community: following users, comments, and direct purchasing of items

## 🗓️ Project Plan & Schedule
The schedule focuses on delivering an MVP in a logical build order, with learning time included.  
Estimates assume ~5–6 hours/day.

| Order | Area / Page | Scope | Estimate (days) | Notes / Acceptance Criteria |
|:--:|---|---|---:|---|
| 1 | **Frontend Sketch & Setup** | Initialize RN/Expo project, folder structure, navigation (Home / Camera / Favorite / Profile), base theme | **1–3** | App launches, tabs work, basic layout and icons ready |
| 2 | **Image Capture & OCR** | Camera permission, Camera, ML Kit OCR, Vision API fallback, Error handling | **5–8** | OCR text extraction reliable; retry flow and UI tested |
| 3 | **Authentication** | Email/Password + Google/Apple login, JWT refresh, profile setup, onboarding | **3–5** | Full login/logout works; tokens refresh; onboarding complete |
| 4 | **Text Processing & Matching** | Text Normalization, Trigram Search, Embeddings | **6–10** | Matching returns top 2–3; confidence scoring visible |
| 5 | **Database** | Schema design, Seed data, Alembic migrations | **3–7** | Catalog entries searchable and linked to matching results |
| 6 | **Home Feed** | Sections: Recommended for You, Bestsellers, Recently Searched, Trending | **3–5** | Feed loads dynamically; empty-state and error handling in place |
| 7 | **Explore / Search Page** | Search by text, category tags, filters, sort options | **3–5** | Debounced search; results render smoothly; no crashes on empty |
| 8 | **Item Listing & Details** | List view with infinite scroll; item details (image, meta, similar items) | **3-5** | Item details show correct info; navigation from Explore works |
| 9 | **Favorite Page** | Sync logic, UI interactions | **2-4** | Favorites persist after relaunch; feedback toast shown |
| 10 | **Profile Page** | Stats visualization, User activity history | **3–5** | Displays personal stats or summary text; editable profile info |
| 11 | **Frontend Design Update** | Apply refined styling, spacing, and responsive layout | **3–5** | Unified visual theme; consistent spacing and color usage |
| 12 | **Monetization & Ads Integration** | AdMob integration (Banner/Native) | **3–5** | Ads load conditionally; can toggle via config (AD_ENABLED=false) |
| 13 | **Backend Glue & APIs** | Middleware, Rate limiting, Documentation| **3–5** | API passes Postman tests |
| 14 | **CI/CD & Monitoring** | CI/CD Pipeline, Monitoring (Sentry)| **1–2** | Auto build/test/deploy; monitoring connected |

> **Total (MVP mid-range):** ~ **35–60 workdays**  
> Focus order: Camera/OCR → Matching → Catalog/Search → Auth → Feed/Favorites → Profile

## 💰 Monetization Plan

- **Phase 1 – Free Tier (Launch)**  
  - Full feature access.
  - Monetized via AdMob Banners (Collection tab) and Native Ads (Detail view).

- **Phase 2 – Ad-Free Tier (Update)**  
  - Removes all advertisements.
  - Unlocks Market Valuation (Price info) and Compatibility Score (User-Item matching). 
  - In-app purchase: **$4.99/month**

- **Phase 3 – Pro Tier (Future)**  
  - Personalized commerce: Direct purchasing of items based on preference analysis.
  - $19.99/month (Subscription or Transactional model)

## 🔒 Repository Visibility
This project’s implementation is currently hosted in a **private repository** for internal development and deployment.  
This public README is shared for portfolio purposes only.

## Getting Started
This project uses Native Modules (ML Kit), so a **Development Build** is required.
```bash
# backend
cd backend
uvicorn app.main:app --reload

# frontend
cd frontend
npm install
npm start
OR
npx expo run:ios
