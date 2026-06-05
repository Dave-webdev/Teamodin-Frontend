# HRStack Frontend

![HRStack Banner](https://via.placeholder.com/1200x300?text=HRStack+Frontend+-+Web+Operating+System+for+SMBs)

HRStack is a lightweight, web-first HR operating system tailored for scaling SMBs (30–200 employees). This repository contains the frontend implementation, delivering a consolidated, premium workspace for employee directories, leave management, onboarding workflows, and performance check-ins.

Designed with a focus on speed, accessibility, and a minimalist, high-end SaaS aesthetic, this frontend serves as the primary interface for both Admin (desktop-first) and Employee (mobile-responsive) users.

---

## Tech Stack

Our frontend architecture is chosen for developer velocity, strict type safety, and optimal client-side performance.

- **Core Framework:** React 18
- **Language:** TypeScript
- **Build Tool:** Vite
- **Styling:** Tailwind CSS
- **Server State Management:** React Query
- **Local State Management:** Zustand
- **Routing:** React Router v6
- **Data Visualization:** Recharts
- **Forms & Validation:** React Hook Form + Zod

---

## Design System & UI/UX Guidelines

To maintain our targeted premium aesthetic, all UI development must adhere to the following standards:

- **Typography:** The primary application font is strictly **Nunito Sans**. Ensure it is loaded optimally to prevent layout shifts.
- **Visual Language:** Prioritize clean whitespace, subtle borders, and a muted, professional color palette. Avoid overly saturated or playful colors.
- **Accessibility:** All core flows, especially the Admin dashboard and Leave Request forms, must meet WCAG 2.1 AA compliance. Charts must be color-blind safe, and tables must use tabular figures.
- **Performance Thresholds:** The interactive Organizational Chart (rendering up to 200 nodes) must execute pan/zoom operations smoothly and load in **under 1 second**.

---

## Getting Started

### Prerequisites

Ensure your local development environment has the following installed:

- Node.js (v18.x or higher)
- npm (v9.x or higher) or yarn (v1.22.x)

### Installation

1. Clone the repository:
   git clone https://github.com/grazac-academy/Teamodin-Frontend.git
   cd hrstack-frontend

2. Install dependencies:
   npm install

3. Configure Environment Variables:
   Duplicate the example environment file and update it with your local development keys.
   cp .env.example .env.local

Required Variables:
VITE_API_BASE_URL=http://localhost:8080/api/v1
VITE_GOOGLE_OAUTH_CLIENT_ID=your_client_id_here
VITE_GA_MEASUREMENT_ID=G-XXXXXXXXXX

4. Start the development server:
   npm run dev

The application will be available at http://localhost:5173.

---

## Project Structure

src/
├── assets/ # Static assets (images, global CSS, Nunito Sans font files)
├── components/ # Global shared UI components (Buttons, Inputs, Modals)
├── config/ # Global configurations (Axios instances, constants)
├── features/ # Feature-based modules (Domain-driven)
│ ├── auth/ # Login, Workspace creation, OAuth
│ ├── directory/ # Employee list, Org Chart, Profiles
│ ├── leave/ # Leave requests, Balances, Manager Approvals
│ ├── onboarding/ # Task checklists, New-hire templates
│ └── analytics/ # eNPS dashboards, Attrition charts
├── hooks/ # Shared custom React hooks
├── layouts/ # Page layout wrappers (DashboardLayout, AuthLayout)
├── lib/ # Third-party library initializations (React Query client)
├── routes/ # Route definitions and lazy loading
├── store/ # Zustand global state stores
├── types/ # Global TypeScript type definitions
└── utils/ # Helper functions, formatters, validators.

---

## Authentication Flow

HRStack utilizes a robust JWT-based authentication system backed by the Spring Boot backend.

1. **Login:** Users authenticate via Email/Password or Google OAuth.
2. **Tokens:** Upon success, the backend returns a short-lived Access Token (15m) and a long-lived Refresh Token (7d).
3. **Interceptors:** The frontend axios instance is configured to automatically intercept 401 responses, attempt a silent token refresh using the Refresh Token, and retry the failed request seamlessly.
4. **Multi-tenancy:** The workspace_id is securely tied to the user session context upon login to ensure data isolation.

---

## Scripts

- npm run dev: Starts the Vite development server.
- npm run build: Compiles TypeScript and builds the app for production.
- npm run preview: Locally previews the production build.
- npm run lint: Runs ESLint to check for code quality and formatting issues.
- npm run typecheck: Runs the TypeScript compiler to check for type errors.

---

## Contribution Guidelines

1. **Branch Naming:** Use the format type/feature-name (e.g., feat/org-chart, fix/leave-modal-overflow).
2. **Commit Messages:** Follow standard conventional commits.
3. **Pull Requests:** Ensure all PRs pass the typecheck and lint scripts. Include screenshots for any UI changes. Assign a reviewer before merging into main.
