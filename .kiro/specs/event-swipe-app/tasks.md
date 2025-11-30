# Implementation Plan

- [ ] 1. Set up project structure and core infrastructure
- [x] 1.1 Create project root structure with separate backend and frontend folders
  - Create /backend folder for Node.js/Express API
  - Create /frontend folder for React application
  - Create root README.md with project overview
  - _Requirements: All_

- [x] 1.2 Initialize Node.js/Express backend with TypeScript configuration
  - Navigate to /backend folder
  - Create package.json with dependencies (express, mongodb, typescript, bcrypt, jsonwebtoken, stripe)
  - Configure TypeScript with tsconfig.json
  - Set up backend folder structure (src/routes, src/services, src/middleware, src/types, src/models)
  - _Requirements: All_

- [ ] 1.3 Set up MongoDB connection and database utilities
  - Create MongoDB connection module with connection pooling in /backend/src/config
  - Implement database initialization with index creation
  - Create utility functions for common database operations
  - _Requirements: All_

- [ ] 1.4 Initialize React frontend with TypeScript
  - Navigate to /frontend folder
  - Create React app with TypeScript template
  - Set up React Router for navigation
  - Configure Axios for API communication
  - Set up frontend folder structure (src/components, src/services, src/hooks, src/types, src/pages)
  - _Requirements: 14.1, 14.2_

- [ ] 1.5 Configure environment variables and secrets management
  - Create /backend/.env.example with required variables (MongoDB URI, JWT secret, Stripe keys)
  - Create /frontend/.env.example with API URL
  - Set up environment configuration loading in both projects
  - _Requirements: 13.1, 13.2_

- [ ] 1.6 Create basic health check endpoint and verify server runs
  - Implement GET /api/health endpoint in /backend
  - Start the backend server and verify it responds
  - _Requirements: All_

- [ ] 2. Implement user authentication system
- [ ] 2.1 Create user registration endpoint
  - Implement POST /api/auth/register endpoint
  - Hash passwords with bcrypt before storage
  - Create Stripe customer on registration
  - Store user data in MongoDB users collection
  - Run the server and test the endpoint works
  - _Requirements: 1.1, 1.2, 1.4, 1.5_

- [ ]* 2.2 Write property test for user registration
  - **Property 1: User registration creates unique identifiers**
  - **Property 2: Profile data persistence**
  - **Property 3: Duplicate email rejection**
  - **Property 4: Password hashing**
  - **Property 5: Stripe customer creation**
  - **Validates: Requirements 1.1, 1.2, 1.3, 1.4, 1.5**

- [ ] 2.3 Create user login endpoint with JWT token generation
  - Implement POST /api/auth/login endpoint
  - Verify password with bcrypt
  - Generate JWT token with expiration
  - Return user data and token
  - Run the server and test the endpoint works
  - _Requirements: 2.1, 2.2, 2.3_

- [ ]* 2.4 Write property test for authentication
  - **Property 6: Valid authentication succeeds**
  - **Property 7: Invalid authentication fails**
  - **Property 8: Session token generation**
  - **Validates: Requirements 2.1, 2.2, 2.3**

- [ ] 2.5 Implement authentication middleware for protected routes
  - Create JWT verification middleware
  - Add error handling for expired/invalid tokens
  - Run the server and test middleware with protected routes
  - _Requirements: 2.3, 2.4_

- [ ]* 2.6 Write property test for logout
  - **Property 9: Logout invalidates session**
  - **Validates: Requirements 2.4**

- [ ] 2.7 Create logout endpoint
  - Implement POST /api/auth/logout endpoint
  - Implement token blacklist or invalidation mechanism
  - Run the server and test logout invalidates tokens
  - _Requirements: 2.4_

- [ ] 2.8 Verify authentication endpoints work by running the server
  - Start the backend server
  - Test registration and login endpoints manually or with curl
  - Verify JWT tokens are generated correctly
  - _Requirements: 1.1, 2.1, 2.3_

- [ ] 2.9 Build registration and login UI components
  - Create RegistrationForm component with profile fields
  - Create LoginForm component
  - Implement form validation
  - Connect to authentication API endpoints
  - _Requirements: 1.1, 1.2, 2.1_

- [ ] 3. Implement organizer profile management
- [ ] 3.1 Create organizer profile creation endpoint
  - Implement POST /api/organizers endpoint
  - Create Stripe connected account
  - Store organizer data with userId reference
  - Run the server and test the endpoint works
  - _Requirements: 7.1, 7.2, 7.3_

- [ ]* 3.2 Write property test for organizer profiles
  - **Property 27: Organizer profile data persistence**
  - **Property 28: Organizer-user association**
  - **Property 29: Stripe connected account creation**
  - **Validates: Requirements 7.1, 7.2, 7.3**

- [ ] 3.3 Implement organizer authorization middleware
  - Create middleware to verify user has organizer profile
  - Add to organizer-only routes
  - Run the server and test authorization works correctly
  - _Requirements: 7.4_

- [ ]* 3.4 Write property test for organizer authorization
  - **Property 30: Organizer authorization**
  - **Validates: Requirements 7.4**

- [ ] 3.5 Verify organizer endpoints work by running the server
  - Start the backend server
  - Test organizer profile creation endpoint
  - Verify authorization middleware works correctly
  - _Requirements: 7.1, 7.4_

- [ ] 3.6 Build organizer profile creation UI
  - Create OrganizerProfileForm component
  - Connect to organizer API endpoint
  - _Requirements: 7.1_

- [ ] 4. Implement event management system
- [ ] 4.1 Create event creation endpoint
  - Implement POST /api/events endpoint (organizer only)
  - Store event with embedded location using GeoJSON format
  - Initialize swipeScore to 0
  - Create 2dsphere index on location.coordinates
  - Run the server and test event creation works
  - _Requirements: 8.1, 8.2, 8.3, 12.1, 12.2_

- [ ]* 4.2 Write property test for event creation
  - **Property 31: Event data persistence**
  - **Property 32: Event associations**
  - **Property 33: Initial swipe score**
  - **Property 48: Location data persistence**
  - **Property 49: Event-location embedding**
  - **Validates: Requirements 8.1, 8.2, 8.3, 12.1, 12.2**

- [ ] 4.3 Create event update and delete endpoints
  - Implement PUT /api/events/:id endpoint (organizer only)
  - Implement DELETE /api/events/:id endpoint (soft delete with isActive flag)
  - Run the server and test update and delete work
  - _Requirements: 8.4, 8.5_

- [ ]* 4.4 Write property test for event updates
  - **Property 34: Event update persistence**
  - **Property 35: Event deletion**
  - **Property 52: Location update in event**
  - **Validates: Requirements 8.4, 8.5, 12.5**

- [ ] 4.5 Create event retrieval endpoints
  - Implement GET /api/events/:id endpoint
  - Implement GET /api/organizers/:id/events endpoint
  - Run the server and test retrieval endpoints work
  - _Requirements: 5.3, 8.1_

- [ ]* 4.6 Write property test for event details
  - **Property 20: Event details are complete**
  - **Property 51: Event details include location**
  - **Validates: Requirements 5.3, 12.4**

- [ ] 4.7 Verify event endpoints work by running the server
  - Start the backend server
  - Test event creation, update, and retrieval endpoints
  - Verify geospatial indexing works correctly
  - _Requirements: 8.1, 8.4, 12.3_

- [ ] 4.8 Build event creation and management UI
  - Create EventCreationForm component with location fields
  - Create EventManagement component for listing organizer events
  - Implement image upload for event photos
  - _Requirements: 8.1, 8.2_

- [ ] 5. Implement ticket type management
- [ ] 5.1 Create ticket type endpoints
  - Implement POST /api/tickets/types endpoint (organizer only)
  - Implement PUT /api/tickets/types/:id endpoint (organizer only)
  - Store ticket types with eventId reference
  - Run the server and test ticket type endpoints work
  - _Requirements: 9.1, 9.2, 9.3_

- [ ]* 5.2 Write property test for ticket types
  - **Property 36: Ticket type data persistence**
  - **Property 37: Ticket type-event association**
  - **Property 38: Ticket type update persistence**
  - **Validates: Requirements 9.1, 9.2, 9.3**

- [ ] 5.3 Verify ticket type endpoints work by running the server
  - Start the backend server
  - Test ticket type creation and update endpoints
  - Verify ticket types are properly associated with events
  - _Requirements: 9.1, 9.2_

- [ ] 5.4 Build ticket type management UI
  - Create TicketTypeManager component
  - Allow organizers to add/edit ticket types for events
  - _Requirements: 9.1, 9.2_

- [ ] 6. Implement event discovery feed
- [ ] 6.1 Create discovery feed endpoint with filtering
  - Implement GET /api/events/feed endpoint
  - Filter by user location using $geoNear or $near operator
  - Exclude past events (endDate < now)
  - Exclude events user has already swiped on
  - Order by swipeScore descending
  - Run the server and test feed filtering works
  - _Requirements: 4.1, 4.2, 4.3, 4.4, 12.3_

- [ ]* 6.2 Write property test for feed filtering
  - **Property 14: Location-based filtering**
  - **Property 15: Past events excluded**
  - **Property 16: Previously swiped events excluded**
  - **Property 17: Feed ordering by swipe score**
  - **Property 50: Distance calculation uses coordinates**
  - **Validates: Requirements 4.1, 4.2, 4.3, 4.4, 12.3**

- [ ] 6.3 Verify discovery feed endpoint works by running the server
  - Start the backend server
  - Test feed endpoint with different user locations
  - Verify geospatial filtering and ordering work correctly
  - _Requirements: 4.1, 4.2, 4.3, 4.4_

- [ ] 6.4 Build discovery feed UI with swipe cards
  - Create SwipeCard component displaying event information
  - Create DiscoveryFeed container managing card stack
  - Implement swipe gesture recognition (left/right)
  - Display empty state when no events available
  - _Requirements: 3.1, 3.4, 4.5, 14.2_

- [ ]* 6.5 Write property test for feed display
  - **Property 10: Feed displays complete event information**
  - **Validates: Requirements 3.1**

- [ ]* 6.6 Write unit test for empty feed edge case
  - Test that empty feed displays appropriate message
  - _Requirements: 4.5_

- [ ] 7. Implement swipe functionality
- [ ] 7.1 Create swipe recording endpoint
  - Implement POST /api/swipes endpoint
  - Store swipe with userId, eventId, direction, timestamp
  - Capture device info and location metadata
  - Prevent duplicate swipes with compound index
  - Run the server and test swipe recording works
  - _Requirements: 3.2, 3.3, 3.5, 11.1, 11.2, 11.3_

- [ ]* 7.2 Write property test for swipe recording
  - **Property 11: Swipe right saves event**
  - **Property 12: Swipe left removes from feed**
  - **Property 13: Swipe records are complete**
  - **Property 44: Swipe metadata capture**
  - **Property 45: Duplicate swipe prevention**
  - **Validates: Requirements 3.2, 3.3, 3.5, 11.2, 11.3**

- [ ] 7.3 Verify swipe endpoint works by running the server
  - Start the backend server
  - Test swipe recording endpoint
  - Verify duplicate prevention works
  - _Requirements: 3.2, 3.3, 11.3_

- [ ] 7.4 Connect swipe UI to swipe endpoint
  - Call swipe API on swipe gesture
  - Update UI to show next card
  - Handle swipe errors
  - _Requirements: 3.2, 3.3, 3.4_

- [ ] 8. Implement saved events functionality
- [ ] 8.1 Create saved events endpoint
  - Implement GET /api/users/:id/saved-events endpoint
  - Query swipes collection for right swipes
  - Populate event details including ticket types
  - Run the server and test saved events retrieval works
  - _Requirements: 5.1, 5.2_

- [ ]* 8.2 Write property test for saved events
  - **Property 18: Saved events match swipe history**
  - **Property 19: Saved events display required fields**
  - **Validates: Requirements 5.1, 5.2**

- [ ] 8.3 Create endpoint to remove saved event
  - Implement DELETE /api/users/:id/saved-events/:eventId endpoint
  - Remove swipe record or mark as removed
  - Run the server and test event removal works
  - _Requirements: 5.4_

- [ ]* 8.4 Write property test for event removal
  - **Property 21: Event removal from saved list**
  - **Validates: Requirements 5.4**

- [ ] 8.5 Verify saved events endpoints work by running the server
  - Start the backend server
  - Test saved events retrieval endpoint
  - Test event removal endpoint
  - _Requirements: 5.1, 5.4_

- [ ] 8.6 Build saved events UI
  - Create SavedEventsList component
  - Display events with ticket information
  - Allow users to remove events
  - _Requirements: 5.1, 5.2, 5.4_

- [ ] 9. Implement ticket purchase system
- [ ] 9.1 Create ticket purchase initiation endpoint
  - Implement POST /api/tickets/purchase endpoint
  - Calculate total amount (price * quantity)
  - Verify ticket availability
  - Create Stripe payment intent
  - Store ticket purchase record with status pending
  - Run the server and test purchase initiation works
  - _Requirements: 6.1, 6.2, 9.4_

- [ ]* 9.2 Write property test for ticket purchase initiation
  - **Property 22: Ticket price calculation**
  - **Property 23: Payment intent creation**
  - **Validates: Requirements 6.1, 6.2**

- [ ]* 9.3 Write unit test for zero inventory edge case
  - Test that purchases are rejected when quantity is zero
  - _Requirements: 9.4_

- [ ] 9.4 Create payment confirmation endpoint
  - Implement POST /api/tickets/purchase/:id/confirm endpoint
  - Verify payment with Stripe
  - Update ticket purchase status to paid or failed
  - Decrement ticket quantity on success
  - Store Stripe payment intent and charge IDs
  - Run the server and test payment confirmation works
  - _Requirements: 6.3, 6.4, 6.5, 9.5, 13.3_

- [ ]* 9.5 Write property test for payment processing
  - **Property 24: Successful payment status**
  - **Property 25: Failed payment status**
  - **Property 26: Ticket inventory decrement**
  - **Property 55: Payment identifiers stored**
  - **Validates: Requirements 6.3, 6.4, 6.5, 9.5, 13.3**

- [ ] 9.6 Create refund endpoint
  - Implement POST /api/tickets/purchase/:id/refund endpoint
  - Process refund through Stripe
  - Update ticket purchase status to refunded
  - Run the server and test refund processing works
  - _Requirements: 13.4_

- [ ]* 9.7 Write property test for refunds
  - **Property 56: Refund processing**
  - **Validates: Requirements 13.4**

- [ ] 9.8 Verify ticket purchase endpoints work by running the server
  - Start the backend server
  - Test ticket purchase initiation endpoint
  - Test payment confirmation endpoint with Stripe test mode
  - Verify inventory decrements correctly
  - _Requirements: 6.1, 6.2, 6.3, 6.5_

- [ ] 9.9 Build ticket purchase UI flow
  - Create TicketPurchaseFlow component
  - Integrate Stripe.js for payment UI
  - Handle payment success and failure states
  - _Requirements: 6.1, 6.2, 6.3, 6.4_

- [ ]* 9.10 Write property test for payment security
  - **Property 53: Stripe payment intent usage**
  - **Property 54: No raw credit card storage**
  - **Property 57: Connected account routing**
  - **Validates: Requirements 13.1, 13.2, 13.5**

- [ ] 10. Implement analytics system
- [ ] 10.1 Create analytics recording functions
  - Implement function to increment view counter
  - Implement function to increment swipe counters
  - Implement function to update purchase analytics
  - Aggregate analytics by date
  - Run the server and test analytics functions work
  - _Requirements: 10.2, 10.3, 10.5_

- [ ]* 10.2 Write property test for analytics updates
  - **Property 40: Swipe analytics increment**
  - **Property 41: Purchase analytics update**
  - **Property 43: View analytics increment**
  - **Property 42: Analytics date aggregation**
  - **Validates: Requirements 10.2, 10.3, 10.4, 10.5**

- [ ] 10.3 Integrate analytics recording into swipe and purchase flows
  - Call analytics functions when swipes are recorded
  - Call analytics functions when purchases complete
  - Call analytics functions when events are viewed
  - Run the server and verify analytics update correctly
  - _Requirements: 10.2, 10.3, 10.5_

- [ ] 10.4 Implement swipe score calculation
  - Create function to calculate swipe score (right swipes / total swipes)
  - Update swipe score when new swipes are recorded
  - Run the server and verify swipe score updates correctly
  - _Requirements: 11.4, 11.5_

- [ ]* 10.5 Write property test for swipe score
  - **Property 46: Swipe score calculation**
  - **Property 47: Swipe score recalculation**
  - **Validates: Requirements 11.4, 11.5**

- [ ] 10.6 Create analytics retrieval endpoint
  - Implement GET /api/events/:id/analytics endpoint (organizer only)
  - Return views, swipes, tickets sold, revenue
  - Run the server and test analytics retrieval works
  - _Requirements: 10.1_

- [ ]* 10.7 Write property test for analytics display
  - **Property 39: Analytics display completeness**
  - **Validates: Requirements 10.1**

- [ ] 10.8 Verify analytics endpoints work by running the server
  - Start the backend server
  - Test analytics retrieval endpoint
  - Verify analytics are updated correctly after swipes and purchases
  - _Requirements: 10.1, 10.2, 10.3_

- [ ] 10.9 Build analytics dashboard UI
  - Create AnalyticsDashboard component
  - Display metrics with charts/graphs
  - Show trends over time
  - _Requirements: 10.1, 10.4_

- [ ] 11. Implement mobile responsiveness and touch gestures
- [ ] 11.1 Add mobile-responsive CSS
  - Implement responsive breakpoints
  - Optimize layout for mobile screens
  - Ensure touch-friendly button sizes
  - _Requirements: 14.1, 14.4_

- [ ] 11.2 Optimize images for mobile
  - Implement image resizing/compression
  - Use responsive image loading
  - _Requirements: 14.3_

- [ ] 11.3 Implement performance optimizations
  - Add code splitting
  - Implement lazy loading for routes
  - Optimize bundle size
  - _Requirements: 14.5_

- [ ] 12. Final checkpoint - Ensure all tests pass
  - Run all property-based tests
  - Run all unit tests
  - Fix any failing tests
  - Verify all core functionality works end-to-end
  - Ask the user if questions arise
