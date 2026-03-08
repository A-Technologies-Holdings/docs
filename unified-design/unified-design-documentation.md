# Unified Repository Design: Melanin Map (The New Legacy Muse)

**Version:** 2.0.0
**Last Updated:** 2026-03-07

## 1. Introduction

This document outlines the unified design for the next generation of the Legacy Muse platform. The goal is to consolidate the extensive features and sophisticated AI capabilities of the `legacy-muse-85933d6a` repository into the modern, mobile-first `Melanin_Map_Mobile` React Native application. The result will be a single, feature-rich, and performant mobile application that fulfills the original vision of Legacy Muse, built on a scalable and maintainable tech stack.

This document serves as the architectural blueprint and development guide for this initiative.

## 2. Target Architecture

The unified application will be built on a modern, mobile-centric stack that prioritizes real-time features, scalability, and a seamless user experience.

### 2.1. High-Level Design

```mermaid
graph TD
    subgraph Mobile App (React Native + Expo)
        A[React Native UI (NativeWind)]
    end

    subgraph Backend (Convex)
        B[Convex Realtime Database]
        C[Convex Functions (TypeScript)]
    end

    subgraph External Services
        D[Google Gemini AI]
        E[ElevenLabs TTS/Voice]
        F[Spotify API]
        G[RevenueCat]
        H[Stripe]
    end

    A --> C
    C --> B
    C --> D
    C --> E
    C --> F
    C --> G
    C --> H
```

### 2.2. Architectural Decisions

- **Frontend:** The application will be a pure React Native application built with Expo. The existing `Melanin_Map_Mobile` codebase will serve as the foundation. All web-specific code from `legacy-muse` will be deprecated.
- **Backend:** Convex will be the sole backend for the application. All backend logic, including data storage, real-time updates, and AI orchestration, will be implemented as Convex Functions. The custom Express server in `Melanin_Map_Mobile` will be deprecated.
- **AI Stack:** All AI-related logic will be encapsulated within Convex backend functions. This provides a secure and scalable way to interact with AI services like Google Gemini and ElevenLabs.
- **Styling:** The UI will be styled using NativeWind and Tailwind CSS, ensuring a consistent and maintainable design system.

## 3. Consolidated Feature Set

The unified application will include the full feature set of `legacy-muse-85933d6a`, ported to the React Native environment. The following is a non-exhaustive list of the key features that will be implemented:

- **Core:**
    - AI-Generated Daily Content (Stories, Facts, Quizzes)
    - Interactive Map for Discovery
    - Journaling & Reflections (with voice support)
    - AI Chat ("Big Mama")
    - Voice Chat
- **Gamification:**
    - Streaks & Achievements
    - Leaderboards (Global & Friends)
    - Quests & Daily Challenges
- **Immersive Experiences:**
    - 3D Interactive Globe
    - AR Museum
    - Discovery Tours with Audio Narration
- **Personalization:**
    - AI Genealogist
    - Global Music Roots (Spotify Integration)
    - Growth Themes & Weekly Recap
- **Community:**
    - Diaspora (Social Feed)
- **Monetization:**
    - Premium Subscriptions (RevenueCat)
    - Digital Store (with Stripe for payments)

## 4. Database Schema

The Convex database schema will be an amalgamation of the schemas from both repositories. The final schema will be designed to support the full, consolidated feature set. The `DATABASE_MIGRATION_PLAN.md` provides a detailed mapping and migration strategy.

## 5. AI & "Big Mama" Persona

The implementation of the "Big Mama" AI persona is a top priority. This will involve:

- **Porting Prompts:** The system prompts and context-specific instructions from `legacy-muse`'s `big-mama-orchestrator` will be ported to a new Convex function.
- **Implementing RAG:** A Retrieval-Augmented Generation (RAG) pipeline will be implemented in Convex to provide the AI with contextual information from the database. This will likely involve using a vector database service that integrates with Convex.
- **AI Orchestration:** A new Convex function will be created to serve as the central AI orchestrator, handling all interactions with the Gemini AI and ensuring the "Big Mama" persona is consistently applied.

## 6. Development Roadmap

The development process will be broken down into the following phases:

1.  **Phase 1: Backend & AI Foundation:**
    - Implement the full database schema in Convex.
    - Port the "Big Mama" AI persona and RAG architecture to Convex.
    - Create the core AI orchestration and content generation functions.
2.  **Phase 2: Core Feature Parity:**
    - Implement the major missing features from `legacy-muse`, including the 3D Globe, AR Museum, and AI Genealogist.
    - Port the full gamification engine (Quests, Leaderboards).
3.  **Phase 3: Community & Personalization:**
    - Implement the Diaspora social feed.
    - Implement the Global Music Roots feature with Spotify integration.
    - Implement the Growth Themes and Weekly Recap features.
4.  **Phase 4: Monetization & Polish:**
    - Implement the Digital Store with Stripe integration.
    - Conduct a full UI/UX review and polish.
    - Perform extensive testing and optimization.

## 7. UI/UX Design System

A unified design system will be created based on the best elements from both repositories. All components will be built using React Native and styled with NativeWind/Tailwind CSS. The existing components in `Melanin_Map_Mobile` will be refactored and expanded to create a comprehensive and reusable component library.
