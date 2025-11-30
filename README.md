# Event Swipe App

A mobile-first web application that combines an intuitive swipe interface with event discovery and ticketing. Users can discover local events through a card-based interface similar to Tinder, save events of interest, and purchase tickets seamlessly.

## Overview

The Event Swipe App enables users to:
- **Discover Events**: Swipe through local events with an intuitive card-based interface
- **Save Favorites**: Swipe right to save events you're interested in attending
- **Purchase Tickets**: Buy tickets directly through the platform with secure Stripe integration
- **Organize Events**: Create and manage events as an organizer with analytics tracking

## Architecture

The application uses a three-tier architecture:

```
┌─────────────────────────────────────┐
│     React Frontend (Mobile-First)   │
│  - Swipe Interface                  │
│  - Event Discovery Feed             │
│  - User/Organizer Dashboards        │
└──────────────┬──────────────────────┘
               │ HTTPS/REST API
┌──────────────▼──────────────────────┐
│     Node.js/Express Backend API     │
│  - Authentication & Authorization   │
│  - Business Logic                   │
│  - Stripe Integration               │
└──────────────┬──────────────────────┘
               │
      ┌────────┴────────┐
      │                 │
┌─────▼─────┐    ┌─────▼──────┐
│  MongoDB  │    │   Stripe   │
│  Database │    │    API     │
└───────────┘    └────────────┘
```

## Project Structure

```
event-swipe-app/
├── backend/          # Node.js/Express API server
│   ├── src/
│   │   ├── routes/   # API route handlers
│   │   ├── services/ # Business logic
│   │   ├── middleware/ # Auth, validation, etc.
│   │   ├── models/   # Data models
│   │   ├── types/    # TypeScript type definitions
│   │   └── config/   # Configuration files
│   └── package.json
│
├── frontend/         # React application
│   ├── src/
│   │   ├── components/ # React components
│   │   ├── pages/    # Page components
│   │   ├── services/ # API communication
│   │   ├── hooks/    # Custom React hooks
│   │   └── types/    # TypeScript type definitions
│   └── package.json
│
└── README.md         # This file
```

## Technology Stack

### Frontend
- React 18+ with TypeScript
- React Router for navigation
- Axios for API communication
- Stripe.js for payment UI
- React Spring or Framer Motion for swipe animations

### Backend
- Node.js with Express.js
- TypeScript for type safety
- JWT for authentication
- Stripe Node SDK for payment processing
- bcrypt for password hashing

### Database
- MongoDB for flexible document storage
- Geospatial queries for location-based event discovery

## Getting Started

### Prerequisites
- Node.js 18+ and npm
- MongoDB instance (local or MongoDB Atlas)
- Stripe account (for payment processing)

### Backend Setup

```bash
cd backend
npm install
cp .env.example .env
# Edit .env with your configuration
npm run dev
```

### Frontend Setup

```bash
cd frontend
npm install
cp .env.example .env
# Edit .env with your API URL
npm start
```

## Key Features

### For Users
- **Swipe-Based Discovery**: Intuitive card interface for browsing events
- **Location Filtering**: See events near you based on your location
- **Save Events**: Build a list of events you're interested in
- **Secure Ticketing**: Purchase tickets with Stripe integration
- **Profile Management**: Customize your interests and preferences

### For Organizers
- **Event Management**: Create, update, and manage events
- **Ticket Types**: Define multiple ticket types with different pricing
- **Analytics Dashboard**: Track views, swipes, and ticket sales
- **Revenue Tracking**: Monitor ticket sales and revenue
- **Stripe Payouts**: Receive payments through Stripe connected accounts

## API Documentation

The backend API provides RESTful endpoints for:
- Authentication (`/api/auth/*`)
- User management (`/api/users/*`)
- Event discovery (`/api/events/*`)
- Swipe tracking (`/api/swipes/*`)
- Ticket management (`/api/tickets/*`)
- Organizer features (`/api/organizers/*`)

See the backend README for detailed API documentation.

## Security

- Password hashing with bcrypt
- JWT-based authentication
- PCI compliance through Stripe (no card data stored)
- HTTPS for all communications
- Input validation and sanitization
- Role-based access control

## Testing

The project uses a dual testing approach:
- **Unit Tests**: Jest for specific examples and edge cases
- **Property-Based Tests**: fast-check for universal property verification

Run tests:
```bash
# Backend tests
cd backend
npm test

# Frontend tests
cd frontend
npm test
```

## License

[Your License Here]

## Contributing

[Your Contributing Guidelines Here]
