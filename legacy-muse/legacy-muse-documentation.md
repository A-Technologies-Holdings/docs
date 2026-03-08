# Legacy Muse (`legacy-muse-85933d6a`) Documentation

**Version:** 1.0.0 (pre-RN refactor)
**Last Updated:** 2026-03-07

## 1. Overview

`legacy-muse-85933d6a` is a sophisticated, AI-powered mobile and web platform designed to celebrate Black excellence through interactive and engaging experiences. It combines a rich historical content database with cutting-edge AI, gamification, and immersive technologies to provide users with a personalized journey of discovery.

### 1.1. Core Features

- **AI Chat Assistant ("Big Mama"):** A context-aware, persona-driven AI for conversations about Black history.
- **3D Interactive Globe:** A `react-globe.gl` implementation for exploring historical facts and events geographically.
- **AR Museum:** A WebXR-based augmented reality experience for viewing 3D historical artifacts.
- **Gamification Engine:** A comprehensive system including a "Legacy Score," streaks, badges, quests, and leaderboards.
- **AI-Powered Content:** Autonomous agents for generating daily facts, stories, and quizzes.
- **Community & Social:** Features like "Diaspora" for social interaction and "Reflections" for personal journaling.
- **Personalization:** AI-driven features like the "AI Genealogist" and "Global Music Roots" to tailor the experience to the user.
- **Monetization:** Premium subscriptions managed via Stripe (web) and RevenueCat (mobile), plus a digital store.

### 1.2. Tech Stack

| Layer | Technology | Purpose |
| :--- | :--- | :--- |
| **Frontend** | React 18, TypeScript, Vite | Modern, fast, and type-safe web application. |
| **Mobile** | React Native (in progress), Capacitor | Cross-platform mobile application. |
| **Backend** | Supabase (PostgreSQL, Edge Functions) | Database, authentication, storage, and serverless logic. |
| **AI Stack** | Vercel AI SDK, Google Gemini 2.5, ElevenLabs | Text generation, speech synthesis, and AI orchestration. |
| **Styling** | Tailwind CSS, shadcn/ui | Utility-first CSS and a component library. |
| **State Management** | Zustand, TanStack Query | Client-side and server-state management. |

## 2. Architecture

### 2.1. High-Level Design

The application is architected as a monorepo containing the web app, the React Native mobile app (in transition), and the backend services. The backend is a hybrid of Vercel Serverless Functions for AI-heavy tasks and Supabase Edge Functions for data-centric operations.

```mermaid
graph TD
    subgraph Frontend
        A[Web App (Vite + React)]
        B[Mobile App (React Native)]
    end

    subgraph Backend
        C[Vercel API Routes]
        D[Supabase Edge Functions]
        E[Supabase Database]
    end

    subgraph External Services
        F[Google Gemini AI]
        G[ElevenLabs TTS]
        H[Stripe]
        I[RevenueCat]
    end

    A --> C
    A --> D
    B --> C
    B --> D
    C --> F
    C --> G
    D --> E
    D --> H
    D --> I
```

### 2.2. Database Schema

The Supabase PostgreSQL database consists of over 80 tables, modeling everything from user profiles and content to social interactions and e-commerce. Key tables include:

- `profiles`, `user_roles`
- `facts`, `events`, `stories`
- `reflections`, `tasks`
- `badges`, `user_badges`, `streaks`, `quests`
- `diaspora_posts`, `diaspora_comments`
- `genealogy_documents`, `family_members`
- `ar_collections`, `ar_markers`
- `music_playlists`, `music_songs`
- `digital_products`, `user_purchases`

For a complete list of tables, refer to the migration files in `supabase/migrations/`.

## 3. AI System

The AI system is a core component of Legacy Muse, centered around the "Big Mama" persona. It is designed to be context-aware, personalized, and engaging.

### 3.1. AI Orchestration

The `big-mama-orchestrator` Supabase function is the heart of the AI system. It takes a `contextType` (e.g., `home_narrative`, `reflection_response`) and user data to generate a personalized response using a specific prompt and the Gemini 2.5 Pro model.

### 3.2. Retrieval-Augmented Generation (RAG)

For the AI Historian chat feature, Legacy Muse uses a RAG pipeline to provide contextually relevant and accurate answers. The process is as follows:

1.  User's chat message is converted into an embedding.
2.  A similarity search is performed against a vector database of historical facts and events (using `pgvector`).
3.  The most relevant documents are retrieved and passed to the Gemini model along with the user's message and the system prompt.
4.  The model generates a response that is grounded in the provided historical context.

### 3.3. Content Generation

Autonomous agents, implemented as scheduled Supabase functions (`daily-discovery-agent`), use the Gemini AI to generate new content (facts, stories, quizzes) on a daily basis, ensuring the app always has fresh content for users.

## 4. Key Features In-Depth

### 4.1. AR Museum

The AR Museum uses the WebXR Device API to create an immersive augmented reality experience. Users can place 3D models of historical artifacts in their real-world environment, view them from all angles, and listen to audio guides.

### 4.2. Global Music Roots

This feature integrates with the Spotify API to provide an interactive journey through the history of Black music. Users can explore different genres, listen to playlists, and learn about the cultural origins of the music.

### 4.3. AI Genealogist

A powerful tool that allows users to build their family tree and research their ancestry. The AI assistant can help users by suggesting potential family connections, analyzing historical documents, and providing research guidance.

## 5. Documentation & Development

The repository contains extensive documentation in the `/docs` directory, covering everything from architecture and features to development workflows and AI strategy. The `AGENT.md` file provides a comprehensive guide for AI agents working on the codebase.

The development process is centered around a branch-per-feature workflow, with a strong emphasis on code quality, testing, and conventional commits.
