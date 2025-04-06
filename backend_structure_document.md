# Backend Structure Document

This document outlines the backend structure for TechTrek, our educational technology platform designed to help non-technical professionals learn and understand technology concepts in a fun and interactive way. The backend is built to support scalability, maintainability, and high performance while ensuring a secure and smooth user experience.

## 1. Backend Architecture

Our backend uses an integrated platform approach to streamline development and reduce maintenance overhead. Key aspects include:

- **Central Platform:** Using Supabase as our core backend service, we leverage its integrated offerings (database, authentication, and storage) which simplifies coordination between various services.
- **Design Patterns & Frameworks:**
  - **Modular Structure:** Code is organized in a modular fashion to separate business logic from infrastructural concerns.
  - **Serverless Functions:** Where needed (e.g., processing notifications and AI hint triggers), serverless functions ensure that the backend scales automatically without worrying about server management.
  - **RESTful API Principles:** Consistent and standardized endpoints facilitate communication with our frontend (React Native) and external services.
- **Scalability & Maintainability:**
  - The architecture supports incremental feature updates, ensuring new tools (like advanced AI recommendations) can be implemented easily.
  - Built with scalability in mind, it leverages Supabase’s cloud infrastructure for dynamic scaling based on load.
- **Performance:**
  - Designed for responsiveness and low latency, especially during content delivery, user authentication, and when triggering AI-powered hints during lessons.

## 2. Database Management

Our primary data management solution is powered by Supabase, which utilizes PostgreSQL as the underlying database for structured data storage. Key points include:

- **Database Technology:**
  - **SQL (Relational Database):** PostgreSQL provides robust relational data management capabilities.
  
- **Data Storage & Organization:**
  - **Structured Data:** User information, lesson details, progress tracking, and gamification elements are stored in well-defined tables.
  - **Data Access Practices:** The database is accessed via secure RESTful APIs and server-side functions ensuring proper data handling and consistency.
  
- **Data Management Practices:**
  - Regular backups and transaction logging are set in place to ensure data integrity.
  - Database indexing and query optimizations are part of the maintenance schedule to support performance under load.

## 3. Database Schema

Below is a human-readable overview of the Data Schema for our SQL/PostgreSQL database along with an example schema layout:

**Tables Overview:**

- **Users Table:** Stores user account details including authentication, profile information, and gamification metrics.
  - Fields: User ID, email, username, hashed password, XP points, current streak, etc.

- **Lessons Table:** Contains details for each lesson or quiz, including content, topic categorization, order in sequence, and interactive elements.
  - Fields: Lesson ID, Topic, Title, Content, Media assets, Difficulty, etc.

- **Progress Table:** Tracks user progress through lessons, quiz scores, milestones, and history of completed lessons.
  - Fields: Record ID, User ID, Lesson ID, completion status, score, date/time, etc.

- **Gamification Table (Badges/Leaderboards):** Manages rewards, badges, and leaderboard rankings.
  - Fields: Record ID, User ID, Badge type, Achievement date, etc.

- **Notifications Table:** Stores scheduled notifications and user-specific settings for mobile reminders.
  - Fields: Notification ID, User ID, notification type, scheduled time, delivery status, etc.

- **CMS/Content Management Table:** For managing dynamic content updates by administrators.
  - Fields: Content ID, Title, Description, lesson associations, last updated timestamp, etc.

**Example SQL Schema (PostgreSQL):**

/* Users Table */
CREATE TABLE users (
    user_id SERIAL PRIMARY KEY,
    email VARCHAR(255) UNIQUE NOT NULL,
    username VARCHAR(100) NOT NULL,
    password_hash VARCHAR(255) NOT NULL,
    xp_points INTEGER DEFAULT 0,
    current_streak INTEGER DEFAULT 0,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

/* Lessons Table */
CREATE TABLE lessons (
    lesson_id SERIAL PRIMARY KEY,
    topic VARCHAR(100) NOT NULL,
    title VARCHAR(255) NOT NULL,
    content TEXT NOT NULL,
    difficulty VARCHAR(50),
    sequence_order INTEGER,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

/* Progress Table */
CREATE TABLE progress (
    progress_id SERIAL PRIMARY KEY,
    user_id INTEGER REFERENCES users(user_id),
    lesson_id INTEGER REFERENCES lessons(lesson_id),
    completion_status BOOLEAN DEFAULT FALSE,
    score DECIMAL(5,2),
    completed_at TIMESTAMP
);

/* Gamification Table */
CREATE TABLE gamification (
    record_id SERIAL PRIMARY KEY,
    user_id INTEGER REFERENCES users(user_id),
    badge VARCHAR(100),
    awarded_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

/* Notifications Table */
CREATE TABLE notifications (
    notification_id SERIAL PRIMARY KEY,
    user_id INTEGER REFERENCES users(user_id),
    type VARCHAR(100),
    scheduled_time TIMESTAMP,
    delivered BOOLEAN DEFAULT FALSE
);

/* CMS Content Table */
CREATE TABLE cms_content (
    content_id SERIAL PRIMARY KEY,
    title VARCHAR(255) NOT NULL,
    description TEXT,
    lesson_id INTEGER REFERENCES lessons(lesson_id),
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

## 4. API Design and Endpoints

The API for TechTrek is designed using RESTful principles. Key endpoints are exposed to facilitate communication between the frontend and backend services. Here are the major endpoints and their purposes:

- **Authentication & User Management:**
  - /auth/signup: For user registration and account creation.
  - /auth/login: For user login and JWT token generation.
  - /auth/logout: For secure user logout and token invalidation.

- **Lessons and Content Delivery:**
  - /lessons: Retrieve a list of available lessons organized by topic and sequence.
  - /lessons/{id}: Get detailed content for a specific lesson including interactive exercises.

- **User Progress & Gamification:**
  - /progress: Update and retrieve the user’s progress with respect to completed lessons and quiz scores.
  - /gamification: Retrieve user badges, achievements, and leaderboard standings.

- **Notifications:**
  - /notifications: Manage and schedule push notifications, including daily reminders and milestone alerts.

- **AI Chatbot Integration:**
  - /ai/hint: Trigger AI-powered hints during lessons and quizzes. This endpoint integrates with multiple AI models (GPT 4o, Claude 3.7 Sonnet, Gemini 2.5 Pro) based on context.

- **CMS Admin Interface:**
  - /admin/content: Admin interface to create, update, or delete lesson contents and manage user feedback.

## 5. Hosting Solutions

TechTrek’s backend is hosted on a cloud-based infrastructure to ensure smooth operation and scalability:

- **Cloud Provider:** Supabase takes care of the database and authentication hosting, minimizing the need for self-managed servers.
- **Benefits of Chosen Hosting:**
  - **Reliability:** The cloud infrastructure provides high uptime and automatic failover configurations.
  - **Scalability:** As the user base grows, resources scale dynamically without manual intervention.
  - **Cost-effectiveness:** Pay-as-you-go model reduces upfront costs and adapts to scale.

## 6. Infrastructure Components

A range of infrastructure components work together to ensure that the backend remains responsive and secure:

- **Load Balancers:** Distribute incoming traffic evenly across the service instances to reduce potential bottlenecks.
- **Caching Mechanisms:** Implemented to cache frequently accessed lesson content and static resources, enhancing response times (for example, using in-memory caching via Supabase functions or external caching if needed).
- **Content Delivery Networks (CDNs):** Utilized to serve static assets (images, media, and cached lesson content) to users quickly regardless of geographic location.
- **Serverless Functions:** Used for real-time processing, such as mobile notifications and AI hint triggers.

## 7. Security Measures

Security is a top priority. The backend employs several industry-standard measures to protect user data and ensure compliance:

- **Authentication & Authorization:**
  - Managed via Supabase’s built-in authentication service supporting email-based sign-up/in and JWT token systems.
  - Role-based access control to ensure that administrative functions are secured.

- **Data Encryption:**
  - All data transmissions are encrypted using TLS.
  - Sensitive data, including passwords, are stored as salted hash values.

- **API Security:**
  - Endpoints are protected by token-based authentication and rate-limiting to mitigate brute force attacks.

- **Compliance:**
  - Implementation of data protection standards to comply with relevant regulations for user privacy.

## 8. Monitoring and Maintenance

To ensure that the backend remains healthy and reliable, we have established the following monitoring and maintenance practices:

- **Monitoring Tools:**
  - Use of analytics services and error monitoring tools like Mixpanel, Firebase Analytics, and Sentry to track performance and quickly address issues.
  - Regular audits of system logs and user activity to detect and address anomalies.

- **Maintenance Strategies:**
  - Scheduled database backups and routine performance tuning.
  - Continuous updates to dependencies and modules to secure against vulnerabilities.
  - Automated alerts to the development team in case of service degradation or outages.

## 9. Conclusion and Overall Backend Summary

In summary, the TechTrek backend is built with a focus on reliability, scalability, and secure data management. Key highlights include:

- **Robust Architecture:** Leveraging Supabase for integrated backend services such as authentication, database, and storage.
- **Efficient Data Management:** A PostgreSQL database with a clearly defined schema that supports lesson content, progress tracking, and gamification.
- **Secure & Responsive API:** RESTful interfaces ensure seamless communication between the frontend and backend, fortified with modern security protocols.
- **Cloud Hosting & Scalable Infrastructure:** Cloud-based hosting, serverless functions, and CDNs work together to guarantee a smooth user experience.
- **Integrated AI and Notifications:** AI-powered hints and mobile notifications add interactive depth to the learning experience.

This backend setup is designed to effectively meet the project’s goals and position TechTrek as a leading educational platform by ensuring data integrity, responsiveness, and a secure user environment.

---

Below is a brief bullet list of key technologies used in the backend:

- Supabase (Backend & Storage)
- PostgreSQL (Database)
- Serverless functions (for notifications and AI hint triggers)
- RESTful API architecture
- Content Delivery Networks (CDNs) and caching mechanisms
- TLS encryption and JWT token-based authentication
- Monitoring tools such as Mixpanel, Firebase Analytics, and Sentry
