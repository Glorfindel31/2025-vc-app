# Climbing Gym App - Development Tasks

This document outlines the development tasks for the Climbing Gym Web App. We are focusing on functionality first, with styling to be added later.

## PHASE 1: SETUP & INTEGRATION

-   **Step 1: Project Initialization & Environment**
    -   [x] Initialize Next.js project (TypeScript, App Router, `src/`, ESLint, Tailwind CSS installed)
    -   [x] Configure VS Code (Open folder, Optional: Gemini Code Assist)
    -   [ ] Set up Supabase Project (on supabase.com)
    -   [ ] Note down Project URL and anon public key
    -   [ ] Configure Environment Variables (`.env.local` for Supabase URL/keys)
    -   [ ] Add `.env.local` to `.gitignore` (ensure it's present)
    -   [ ] Install Supabase Client Library (`@supabase/supabase-js`)
    -   [ ] Install Supabase Server-Side Rendering Helpers (`@supabase/ssr`)
    -   [ ] Initialize Supabase Client Instances (using `@supabase/ssr` helpers for browser, server components, route handlers)

## PHASE 2: DATABASE SCHEMA

-   **Step 2: Define Supabase Database Tables & Security**
    -   [ ] Define `profiles` table (linked to `auth.users` via `user_id` PK/FK, stores username, full_name, etc.)
    -   [ ] Define `routes` table (name, grade, setter, location, description, image_url?, active_status, etc.)
    -   [ ] Define `attempts` table (user_id FK -> profiles, route_id FK -> routes, success boolean, timestamp, notes?)
    -   [ ] Define Relationships/Foreign Keys between tables in Supabase UI/SQL
    -   [ ] Implement Row Level Security (RLS) policies for all tables (CRITICAL for security - e.g., users can only update their own profile, logged-in users can insert attempts, etc.)
    -   [ ] (Optional) Create Database Functions/Triggers if needed (e.g., trigger to create a profile when a new auth user signs up)

## PHASE 3: AUTHENTICATION

-   **Step 3: Implement User Authentication Flow**
    -   [ ] Create Authentication UI Components/Pages (Layout, Forms - NO STYLING)
        -   [ ] Signup Page (`src/app/signup/page.tsx`)
        -   [ ] Login Page (`src/app/login/page.tsx`)
        -   [ ] Basic Header/Nav Component showing auth state (e.g., display email, show Login/Signup or Logout button)
    -   [ ] Implement Supabase Auth Logic (using client instance from `@supabase/ssr`)
        -   [ ] Handle user signup (`supabase.auth.signUp`) in a form action or client component
        -   [ ] Handle user login (`supabase.auth.signInWithPassword`)
        -   [ ] Handle user logout (`supabase.auth.signOut`)
    -   [ ] Manage User Session State (Leverage `@supabase/ssr` helpers for reading session in Server Components and client-side)
    -   [ ] Implement Route Protection (`middleware.ts` to check auth state for protected pages like adding attempts)

## PHASE 4: CORE FEATURES - ROUTES

-   **Step 4: Route Management & Display**
    -   [ ] Create UI to Display List of Routes (`src/app/routes/page.tsx`)
        -   [ ] Fetch active routes data from Supabase (using server component client)
        -   [ ] Render route list using plain HTML elements (`<ul>`, `<li>`, `<p>`, etc.)
    -   [ ] Create UI to Add New Route (`src/app/add-route/page.tsx` - consider auth protection later)
        -   [ ] Build simple HTML form for route details
        -   [ ] Implement logic (Server Action?) to insert route data into Supabase
    -   [ ] (Optional Later) UI/Logic for Editing/Deactivating Routes

## PHASE 5: CORE FEATURES - ATTEMPTS

-   **Step 5: Attempt Logging & Viewing**
    -   [ ] Create UI for Logging a New Attempt (e.g., component on a route details page or dedicated `/log-attempt` page)
        -   [ ] Form component (Select Route [maybe dropdown fetched from DB], Mark Success checkbox, Notes textarea)
        -   [ ] Implement logic (Server Action?) to insert attempt data into Supabase (associate with logged-in user's ID and selected route ID)
    -   [ ] Create UI to Display User's Own Attempts (`src/app/my-attempts/page.tsx` or profile page section)
        -   [ ] Fetch attempts data for the _currently logged-in user_ from Supabase
        -   [ ] Render list of user's attempts (plain HTML)

## PHASE 6: RANKING & ENHANCEMENTS

-   **Step 6: Route Ranking Logic (Initial version may be simple display)**
    -   [ ] Display basic route information (covered in step 4)
    -   [ ] (Future) Define ranking criteria (e.g., based on attempts, success rate, grade difficulty)
    -   [ ] (Future) Implement backend logic (DB view/function?) or frontend logic to calculate/display rank
    -   [ ] (Future) Enhance route display pages with ranking information

## PHASE 7: DEPLOYMENT

-   **Step 7: Deploy Application to Vercel**
    -   [ ] Ensure code is pushed to a Git repository (GitHub/GitLab/Bitbucket)
    -   [ ] Create Vercel Project and link repository
    -   [ ] Configure Environment Variables in Vercel Project Settings (for `NEXT_PUBLIC_SUPABASE_URL`, `NEXT_PUBLIC_SUPABASE_ANON_KEY`)
    -   [ ] Trigger deployment & verify live site functionality

## PHASE X: STYLING (Post-Functionality)

-   **Step 8: Apply Styling**
    -   [ ] Systematically apply Tailwind CSS classes to components/pages
    -   [ ] Refine layout, responsiveness, and overall visual appearance
