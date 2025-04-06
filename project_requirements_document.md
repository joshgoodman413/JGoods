# TechTrek Project Requirements Document

## 1. Project Overview

TechTrek is an educational technology platform designed to teach non-technical professionals the basics of technology in a fun, interactive, and gamified manner. Inspired by DuoLingo, this mobile app (for both iOS and Android) delivers short lessons under 10 minutes with activities like drag-and-drop exercises, fill-in-the-blanks, multiple choice, and matching games. By breaking down complex technical concepts into enjoyable, bite-sized learning sessions, TechTrek aims to empower professionals in sales, marketing, product management, project management, and executive leadership to confidently engage with technical teams and make informed decisions.

The platform is being built to address a common challenge: non-technical professionals often struggle to grasp essential technical concepts despite needing them for their day-to-day responsibilities. The key objectives are to ensure that every lesson builds upon the previous one, monitor progress through quizzes, and maintain user engagement with gamification elements such as XP points, streak tracking, badges, and leaderboards. Success will be measured by user progress, lesson completion rates, quiz success, and overall user satisfaction with the learning experience.

## 2. In-Scope vs. Out-of-Scope

**In-Scope:**

*   Development of a mobile app for both iOS and Android devices.
*   Short, interactive, gamified lessons that last less than 10 minutes each.
*   Lessons that include various interactive elements (info slides, drag-and-drop, fill in the blank, tap-to-build, multiple choice, and matching).
*   Structured, sequential learning paths with flexibility to review past lessons or skip ahead upon mastery.
*   Quizzes at the end of every lesson with a mechanism to force a retake after two failed attempts.
*   User account management with email-based sign-up/in.
*   Progress-tracking dashboard with metrics including XP points, streaks, badges, and leaderboards.
*   Push notifications for daily learning reminders, quiz results, and milestone achievements.
*   Offline functionality with local caching of lessons and synchronization with the central database.
*   An admin interface or content management system for updating lessons, quizzes, and managing user feedback.
*   Integration of an AI-powered chatbot that provides hints and guidance throughout lessons and quizzes.

**Out-of-Scope (for initial release):**

*   Quantum computing, advanced engineering principles, or other highly specialized tech topics.
*   Deep personalization through advanced AI recommendations (planned for future updates).
*   Calendar syncing with personal calendars for scheduling lessons or notifications.
*   Extensive third-party analytics integration beyond initial analytics tools like Mixpanel or Firebase Analytics.
*   Multi-language support beyond the primary language (English) in the first version.

## 3. User Flow

When a new user downloads TechTrek, they are welcomed by a clean and inviting sign-up or log-in screen that uses the platform’s signature blue, green, and gray color palette. The onboarding process guides users through the registration, where they not only set up their account via email but also select their preferred timing for daily notifications. After registration, users are walked through the app’s key features and the benefits of offline accessibility, ensuring that lessons and quizzes are available even without an internet connection.

After successful sign-up, users land on the home screen that introduces TechTrek and highlights their learning journey. Navigating through a well-designed learning path, they select topics—ranging from Basics to focused segments like Binary and Operating Systems—and begin interactive lessons. Each lesson is followed by a quiz that provides immediate feedback, with options to use an AI-powered hint button if needed. The journey continues with a progress dashboard displaying completed lessons, XP points, streaks, badges, and leaderboards, reinforcing engagement with periodic mobile notifications.

## 4. Core Features (Bullet Points)

*   **User Authentication & Account Management:**

    *   Email-based sign-up/sign-in
    *   Profile management with personal settings

*   **Interactive Learning Modules:**

    *   Short lessons (<10 minutes) with interactive elements (drag-and-drop, fill in the blank, tap-to-build, multiple choice, matching)
    *   Sequential lessons categorized by topics (e.g., Basics, Binary, Operating Systems)
    *   AI-powered hint mechanism on every page to support users

*   **Quiz & Lesson Progression:**

    *   End-of-lesson quizzes with immediate feedback
    *   Rules for retaking lessons after two failed attempts
    *   Option to review or skip ahead after achieving high quiz scores (e.g., 90% or above)

*   **Gamification & Engagement:**

    *   XP points, streak tracking, badges, and leaderboards
    *   Rewards (e.g., hints, unlockable content) for milestone completion
    *   Daily push notifications for reminders, quiz results, and milestone achievements

*   **Offline Capability:**

    *   Locally cached lessons and quizzes accessed without an internet connection
    *   Synchronization of user progress with the central database upon reconnection

*   **Progress-Tracking Dashboard:**

    *   Detailed metrics on completed lessons, topics, XP, and streaks
    *   Visual progress indicators for each learning path segment

*   **Admin Interface / Content Management System (CMS):**

    *   Centralized platform for updating and managing lesson content, quizzes, and user feedback

*   **Analytics & User Feedback:**

    *   Integration with tools like Mixpanel or Firebase Analytics for tracking user engagement and performance
    *   User feedback collection features for continuous improvement

## 5. Tech Stack & Tools

*   **Frontend:**

    *   React Native (using TypeScript) for building cross-platform mobile apps
    *   UI components styled with a consistent blue, green, and gray palette
    *   Integration with V0 by Vercel for frontend component building

*   **Backend & Storage:**

    *   Supabase for managing database, authentication, and storage
    *   Local caching via React Native’s local storage solutions for offline functionality

*   **AI & Chatbot Integration:**

    *   Incorporation of GPT 4o and Claude 3.7 Sonnet for powering the in-app AI chatbot, which provides real-time hints and guidance during lessons

*   **Development & IDE Tools:**

    *   Lovable.dev for generating front-end and full-stack components
    *   Windsurf and Cursor for integrated AI coding support in the development process
    *   VS Code for code editing, utilizing extensions to optimize productivity

## 6. Non-Functional Requirements

*   **Performance:**

    *   The app should load within 2–3 seconds on both iOS and Android devices.
    *   Online lessons and quizzes need to provide near-instant feedback (within 1 second).

*   **Security:**

    *   All user data must be securely transmitted using HTTPS.
    *   Robust authentication and authorization measures via Supabase.
    *   Safeguarding user progress and personal data with adherence to privacy standards.

*   **Reliability & Usability:**

    *   The offline mode must provide seamless transitions between online and offline status.
    *   The UI/UX should be intuitive, ensuring ease of use for non-technical professionals.
    *   High accessibility standards (clear text, readable fonts, and responsive layouts) should be maintained.

*   **Scalability:**

    *   The system must handle a growing number of users and lessons while maintaining performance.
    *   The architecture should allow for future integrations like advanced AI recommendations and calendar syncing.

## 7. Constraints & Assumptions

*   **Constraints:**

    *   The app’s core functionality is tied to the availability of reliable online services (Supabase, push notifications).
    *   Offline capability must sync effectively without data conflicts.
    *   Reliance on third-party AI models (GPT 4o, Claude 3.7 Sonnet) may be affected by API rate limits or availability.

*   **Assumptions:**

    *   Users have basic mobile literacy even if they lack a technical background.
    *   Content creation (lessons and quizzes) is managed by a single content creator initially, with room for growth.
    *   The sequential curriculum structure will sufficiently address learning gaps, while expert users can opt to skip lessons after mastery.
    *   Future updates may build upon the initial tech stack and user engagement strategies without overhauling the core system.

## 8. Known Issues & Potential Pitfalls

*   **Technical Hurdles:**

    *   Potential challenges in synchronizing offline data with the central database could lead to data conflicts.
    *   Ensuring the AI chatbot’s responses remain accurate, contextually appropriate, and timely as users engage with dynamic content may be complex.
    *   Managing the balance between structured, sequential lessons and user flexibility (skipping or reviewing content) without causing user confusion.

*   **Mitigation Guidelines:**

    *   Implement robust error-handling and clear synchronization protocols for offline data.
    *   Test the AI hint system extensively using real user scenarios to fine-tune response accuracy and helpfulness.
    *   Design user flows with clear navigation cues and easy access to lesson information so that the learning process remains straightforward.
    *   Monitor API usage and prepare fallback mechanisms if third-party AI or analytics services face rate limits or outages.

This document provides a detailed yet easy-to-understand overview of the TechTrek platform requirements. It should guide the development process ensuring that every component of the platform, from interactive lessons to backend services, is aligned with the vision of creating a fun, engaging, and effective educational tool for non-technical professionals.
