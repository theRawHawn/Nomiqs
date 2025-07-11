# replit.md

## Overview

This is a full-stack web application built for TaxNBooks, an accounting firm serving businesses in Tier 2 and Tier 3 cities across India. The application is a modern single-page marketing website with contact form functionality, built using React/TypeScript frontend and Express.js backend.

## User Preferences

Preferred communication style: Simple, everyday language.

## System Architecture

The application follows a monorepo structure with clear separation between client, server, and shared code:

### Frontend Architecture
- **Framework**: React 18 with TypeScript
- **Build Tool**: Vite for fast development and optimized builds
- **Routing**: Wouter for lightweight client-side routing
- **UI Framework**: Shadcn/ui components built on Radix UI primitives
- **Styling**: Tailwind CSS with custom design system
- **State Management**: TanStack Query for server state management
- **Form Handling**: React Hook Form with Zod validation

### Backend Architecture
- **Runtime**: Node.js with Express.js framework
- **Language**: TypeScript with ES modules
- **Database**: PostgreSQL with Drizzle ORM
- **Database Provider**: Neon Database (serverless PostgreSQL)
- **Schema Management**: Drizzle Kit for migrations
- **Validation**: Zod schemas shared between client and server

### Data Storage Strategy
- **Primary Database**: PostgreSQL via Neon Database
- **ORM**: Drizzle ORM for type-safe database operations
- **Development Storage**: In-memory storage implementation for development/testing
- **Schema**: Shared TypeScript types generated from Drizzle schemas

## Key Components

### Frontend Components
- **Landing Page**: Single-page marketing site with multiple sections
- **Contact Form**: React Hook Form with validation and submission handling
- **UI Components**: Comprehensive set of reusable components from Shadcn/ui
- **Navigation**: Smooth scrolling single-page navigation
- **Responsive Design**: Mobile-first design with Tailwind CSS

### Backend Services
- **Contact API**: RESTful endpoint for contact form submissions
- **Storage Interface**: Abstracted storage layer supporting both memory and database implementations
- **Error Handling**: Centralized error handling with proper HTTP status codes
- **Request Logging**: Custom middleware for API request logging

### Database Schema
- **Users Table**: Basic user management (id, username, password)
- **Contact Submissions Table**: Contact form data storage (name, mobile, business_type, message, created_at)
- **Type Safety**: Full TypeScript integration with Drizzle-generated types

## Data Flow

1. **Contact Form Submission**:
   - User fills out contact form on frontend
   - React Hook Form validates data using shared Zod schema
   - Form submission triggers TanStack Query mutation
   - POST request sent to `/api/contact` endpoint
   - Backend validates data again using same Zod schema
   - Data stored in PostgreSQL via Drizzle ORM
   - Success/error response returned to frontend
   - Toast notification shown to user

2. **Admin Data Access**:
   - GET `/api/contact-submissions` endpoint for retrieving submissions
   - Currently no authentication (intended for future admin panel)

## External Dependencies

### Core Runtime Dependencies
- **React Ecosystem**: React 18, React DOM, React Hook Form
- **Backend**: Express.js, Node.js
- **Database**: Drizzle ORM, Neon Database client
- **Validation**: Zod for schema validation
- **UI Libraries**: Radix UI primitives, Lucide React icons
- **Styling**: Tailwind CSS, class-variance-authority for component variants

### Development Tools
- **Build Tools**: Vite, esbuild for production builds
- **Type Checking**: TypeScript compiler
- **Database Tools**: Drizzle Kit for schema management
- **Replit Integration**: Replit-specific plugins for development environment

### Third-party Services
- **Database Hosting**: Neon Database (serverless PostgreSQL)
- **Deployment**: Configured for Replit hosting environment

## Deployment Strategy

### Development Environment
- **Replit Integration**: Configured for Replit development environment
- **Hot Reloading**: Vite dev server with HMR enabled
- **Database**: Uses Neon Database even in development
- **Environment Variables**: DATABASE_URL required for database connection

### Production Build
- **Frontend**: Vite builds static assets to `dist/public`
- **Backend**: esbuild bundles server code to `dist/index.js`
- **Asset Serving**: Express serves static files in production
- **Database Migrations**: Drizzle Kit handles schema updates

### Configuration Files
- **Vite Config**: Handles React build, path aliases, and Replit-specific plugins
- **Drizzle Config**: Database connection and migration settings
- **Tailwind Config**: Custom design system with CSS variables
- **TypeScript Config**: Shared types and path mapping

The application is designed to be easily deployable on Replit with minimal configuration, requiring only the DATABASE_URL environment variable to be set.