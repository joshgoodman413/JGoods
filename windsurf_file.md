# .windsurfrules

## Project Overview

*   **Type:** Mobile educational technology platform
*   **Description:** A mobile app for teaching non-technical professionals (sales, marketing, product management, etc.) basic technology concepts through interactive, gamified lessons with quizzes and AI-driven hints.
*   **Primary Goal:** Empower users to communicate effectively with technical teams and make informed business decisions.

## Project Structure

### Framework-Specific Routing

*   **Directory Rules:**

    *   [React Native + React Navigation 6]: Use a modular navigation structure with a dedicated navigation directory.
    *   Example: "React Navigation 6" → `src/navigation/` utilizing stack and tab navigators.

### Core Directories

*   **Versioned Structure:**

    *   `src/screens`: Contains screen components for lessons, quizzes, dashboard, and authentication.
    *   `src/components`: Houses reusable UI components and interactive exercise modules (drag-and-drop, fill-in-the-blank, etc.).
    *   `src/assets`: Stores images, fonts, and color schemes (blue, green, gray branding).
    *   `src/services`: Manages API calls to Supabase and integrations with AI models (GPT 4o, Claude 3.7 Sonnet, Gemini 2.5 Pro).

### Key Files

*   **Stack-Versioned Patterns:**

    *   `App.tsx`: Root file initializing navigation and global providers (theme, authentication context).
    *   `src/navigation/index.ts`: Configures React Navigation with stack and tab navigators for core app flows (auth, lessons, progress tracking).
    *   `src/screens/LessonScreen.tsx`: Implements lesson rendering with interactive exercises and integrated AI chatbot hints.

## Tech Stack Rules

*   **Version Enforcement:**

    *   [react-native@0.72]: Adhere to latest React Native best practices; ensure use of TypeScript and hooks.
    *   [react-navigation@6]: Enforce usage of stack and tab navigators without mixing with legacy navigation systems.
    *   [supabase]: Follow Supabase guidelines for database access, authentication, and offline sync mechanisms.

## PRD Compliance

*   **Non-Negotiable:**

    *   "Lessons must be short (< 10 minutes), interactive, and feature adaptive quiz logic (two failed attempts lead to lesson repetition) with offline access capabilities."
    *   "Push notifications for daily reminders and achievement alerts must be integrated as per provided specifications."

## App Flow Integration

*   **Stack-Aligned Flow:**

    *   Example: "Authentication Flow → `src/screens/Auth/Login.tsx` for email sign-in, integrated with Supabase auth, followed by redirection to the dashboard at `src/screens/Dashboard.tsx`."
    *   Example: "Lesson Flow → `src/screens/LessonScreen.tsx` handles sequential lesson delivery with quiz integration and AI chatbot hints triggered from each page."
