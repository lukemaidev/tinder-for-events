# Event Swipe Backend

Backend API for the Event Swipe App built with Node.js, Express, and TypeScript.

## Project Structure

```
backend/
├── src/
│   ├── routes/       # API route handlers
│   ├── services/     # Business logic services
│   ├── middleware/   # Express middleware functions
│   ├── types/        # TypeScript type definitions
│   ├── models/       # Data models and schemas
│   └── index.ts      # Application entry point
├── dist/             # Compiled JavaScript (generated)
├── package.json      # Dependencies and scripts
├── tsconfig.json     # TypeScript configuration
└── jest.config.js    # Jest testing configuration
```

## Setup

1. Install dependencies:
```bash
npm install
```

2. Create a `.env` file with required environment variables (see `.env.example`)

3. Build the project:
```bash
npm run build
```

4. Run in development mode:
```bash
npm run dev
```

5. Run in production mode:
```bash
npm start
```

## Testing

Run tests:
```bash
npm test
```

Run tests in watch mode:
```bash
npm run test:watch
```

## Dependencies

- **express**: Web framework
- **mongodb**: MongoDB driver
- **typescript**: TypeScript compiler
- **bcrypt**: Password hashing
- **jsonwebtoken**: JWT authentication
- **stripe**: Payment processing
- **dotenv**: Environment variable management
- **cors**: CORS middleware

## Development Dependencies

- **ts-node**: TypeScript execution for development
- **jest**: Testing framework
- **ts-jest**: TypeScript support for Jest
- **fast-check**: Property-based testing library
