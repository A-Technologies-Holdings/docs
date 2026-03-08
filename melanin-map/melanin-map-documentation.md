# Melanin Map (`Melanin_Map_Mobile`) Documentation

**Version:** 1.0.0
**Last Updated:** 2026-03-07

## 1. Overview

`Melanin_Map_Mobile` is a premium, iOS-first cultural discovery mobile application designed to help users explore Black excellence across place, time, and knowledge. Built as a fast-moving scout MVP, the app validates core engagement loops that will power the future Legacy Muse mobile platform. It is built with React Native and Expo, using Convex as its backend.

### 1.1. Core Features

- **AI-Generated Content:** The app features AI-generated stories and quizzes about Black history, delivered daily.
- **Interactive Map:** Users can explore a map to discover nearby historical landmarks and points of interest.
- **Journaling & Reflections:** A personal space for users to record their thoughts and reflections, with the option to use voice-to-text.
- **Gamification:** The app includes streaks and achievements to encourage daily engagement.
- **AI Chat ("Big Mama"):** A chat interface for interacting with an AI assistant.
- **Voice Chat:** A real-time voice conversation feature using ElevenLabs.

### 1.2. Tech Stack

| Layer | Technology | Purpose |
| :--- | :--- | :--- |
| **Mobile** | React Native, Expo | Cross-platform mobile application development. |
| **Backend** | Convex | Realtime database and serverless functions. |
| **AI Stack** | Custom Express Server, Google Gemini, ElevenLabs | AI-powered content generation and voice features. |
| **Styling** | NativeWind, Tailwind CSS | Utility-first styling for React Native. |
| **State Management** | Zustand, TanStack Query | Client-side and server-state management. |

## 2. Architecture

### 2.1. High-Level Design

Melanin Map is a self-contained Expo application. It includes a custom Express server running within the application to handle AI service calls, which then communicate with external AI providers. The primary backend for data storage and real-time updates is Convex.

```mermaid
graph TD
    subgraph Mobile App (Expo)
        A[React Native UI]
        B[Custom Express Server]
    end

    subgraph Backend
        C[Convex Database]
    end

    subgraph External Services
        D[Google Gemini AI]
        E[ElevenLabs TTS/Voice]
    end

    A --> B
    A --> C
    B --> D
    B --> E
```

### 2.2. Database Schema

The Convex database schema is defined in `convex/schema.ts` and is much simpler than Legacy Muse's. It includes the following collections:

- `profiles`: User profiles and onboarding information.
- `reflections`: User journal entries.
- `tasks`: User tasks.
- `spotlights`: Daily featured content.
- `savedPlaces`, `savedStories`: User bookmarks.
- `achievements`: Unlocked badges.
- `streaks`: User engagement streaks.

## 3. AI System

The AI system in Melanin Map is primarily focused on content generation and voice interaction.

### 3.1. Content Generation

The `/server/ai-facts.ts` file contains the logic for generating stories and quizzes using the Gemini AI. It makes direct calls to the OpenAI-compatible endpoint for Gemini to generate content based on the current date.

### 3.2. Voice Features

The application integrates with ElevenLabs for two key voice features:

- **Text-to-Speech (TTS):** The `/server/ai/service.ts` file includes a function to generate audio narrations of text content.
- **Voice Chat:** The `voice-chat.tsx` screen uses the `@elevenlabs/react-native` package to create a real-time voice conversation with an AI agent.

## 4. Development

The application is a standard Expo project. The main application logic is in the `/app` directory, with components in `/components`, hooks in `/hooks`, and the Convex backend code in `/convex`.

The custom Express server for AI services is located in the `/server` directory. This server is responsible for handling requests from the app, calling the appropriate AI services, and returning the results.
