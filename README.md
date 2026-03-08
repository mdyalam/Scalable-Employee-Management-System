# Objection Auth Task

[![NestJS](https://img.shields.io/badge/NestJS-E0234E?style=for-the-badge&logo=nestjs&logoColor=white)](https://nestjs.com/)
[![TypeScript](https://img.shields.io/badge/TypeScript-007ACC?style=for-the-badge&logo=typescript&logoColor=white)](https://www.typescriptlang.org/)
[![PostgreSQL](https://img.shields.io/badge/PostgreSQL-316192?style=for-the-badge&logo=postgresql&logoColor=white)](https://www.postgresql.org/)
[![JWT](https://img.shields.io/badge/JWT-000000?style=for-the-badge&logo=jsonwebtokens&logoColor=white)](https://jwt.io/)

A robust authentication and user management system built with NestJS, featuring role-based access control, JWT authentication, and comprehensive user operations.

## Description

This project implements a complete authentication system with user management capabilities. It includes user registration, login, profile management, role-based permissions, and administrative features like user listing, updating, and deletion. The system uses Objection.js as the ORM with Knex for database operations and PostgreSQL as the database.

## Features

- 🔐 **JWT Authentication**: Secure token-based authentication
- 👥 **Role-Based Access Control**: Admin, Manager, and Employee roles
- 📧 **Email Integration**: Account activation, locking notifications, and welcome emails
- 📊 **User Management**: CRUD operations on users with pagination and search
- 📈 **Audit Logging**: Login attempt logging and account status tracking
- 📄 **Data Export**: CSV export functionality for user data
- 🛡️ **Security Features**: Password hashing, rate limiting, input validation
- 🗄️ **Database Migrations**: Version-controlled database schema management
- 🧪 **Comprehensive Testing**: Unit and E2E tests with Jest

## Tech Stack

- **Framework**: [NestJS](https://nestjs.com/) - Progressive Node.js framework
- **Language**: [TypeScript](https://www.typescriptlang.org/)
- **Database**: [PostgreSQL](https://www.postgresql.org/)
- **ORM**: [Objection.js](https://vincit.github.io/objection.js/) with [Knex.js](https://knexjs.org/)
- **Authentication**: [Passport.js](https://www.passportjs.org/) with JWT strategy
- **Validation**: [Joi](https://joi.dev/) for request validation
- **Email**: [Nodemailer](https://nodemailer.com/) with Handlebars templates
- **Testing**: [Jest](https://jestjs.io/) for unit and E2E tests
- **Linting**: [ESLint](https://eslint.org/) with Prettier

## Prerequisites

Before running this application, make sure you have the following installed:

- [Node.js](https://nodejs.org/) (v18 or higher)
- [pnpm](https://pnpm.io/) package manager
- [PostgreSQL](https://www.postgresql.org/) database server

## Installation

1. **Clone the repository**
   ```bash
   git clone <repository-url>
   cd objection-auth-task
   ```

2. **Install dependencies**
   ```bash
   pnpm install
   ```

## Environment Setup

Create a `.env` file in the root directory with the following variables:

```env
# Database Configuration
DB_HOST=localhost
DB_PORT=5432
DB_USERNAME=your_db_username
DB_PASSWORD=your_db_password
DB_NAME=your_db_name

# JWT Configuration
JWT_SECRET=your_jwt_secret_key

# Email Configuration
MAIL_HOST=smtp.gmail.com
MAIL_PORT=587
MAIL_USER=your_email@gmail.com
MAIL_PASS=your_app_password

# Application Configuration
PORT=3000
NODE_ENV=development
```

## Database Setup

1. **Create PostgreSQL database**
   ```sql
   CREATE DATABASE your_db_name;
   ```

2. **Run migrations**
   ```bash
   npx knex migrate:latest
   ```

3. **Run seeders (if any)**
   ```bash
   npx knex seed:run
   ```

## Running the Application

### Development Mode
```bash
pnpm run start:dev
```

### Production Mode
```bash
pnpm run build
pnpm run start:prod
```

### Debug Mode
```bash
pnpm run start:debug
```

The application will be available at `http://localhost:3000` (or the port specified in your `.env` file).

## API Endpoints

### Authentication
- `POST /auth/signup` - User registration
- `POST /auth/signin` - User login
- `GET /auth/profile` - Get user profile (authenticated)

### User Management (Admin/Manager only)
- `POST /auth/add-employee` - Add new employee
- `GET /auth/users` - Get all users with pagination and filters
- `PUT /auth/users/:id` - Update user (self or admin/manager)
- `DELETE /auth/users/:id` - Delete user (admin only)
- `GET /auth/export/csv` - Export users to CSV

### Request/Response Examples

#### Sign Up
```bash
POST /auth/signup
Content-Type: application/json

{
  "email": "user@example.com",
  "password": "password123",
  "firstName": "John",
  "lastName": "Doe",
  "role": "Employee"
}
```

#### Sign In
```bash
POST /auth/signin
Content-Type: application/json

{
  "email": "user@example.com",
  "password": "password123"
}
```

Response:
```json
{
  "access_token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...",
  "user": {
    "id": 1,
    "email": "user@example.com",
    "firstName": "John",
    "lastName": "Doe",
    "role": "Employee"
  }
}
```

## Testing

### Unit Tests
```bash
pnpm run test
```

### E2E Tests
```bash
pnpm run test:e2e
```

### Test Coverage
```bash
pnpm run test:cov
```

### Watch Mode
```bash
pnpm run test:watch
```

## Scripts

- `pnpm run build` - Build the application
- `pnpm run format` - Format code with Prettier
- `pnpm run lint` - Lint code with ESLint
- `pnpm run start` - Start the application
- `pnpm run start:dev` - Start in development mode with watch
- `pnpm run start:prod` - Start in production mode
- `pnpm run test` - Run unit tests
- `pnpm run test:e2e` - Run E2E tests

## Project Structure

```
src/
├── app.module.ts          # Main application module
├── main.ts                # Application entry point
├── auth/                  # Authentication module
│   ├── auth.controller.ts
│   ├── auth.service.ts
│   ├── auth.module.ts
│   ├── jwt.strategy.ts
│   ├── roles.decorator.ts
│   ├── roles.guard.ts
│   └── dto/               # Data transfer objects
├── common/                # Shared utilities
│   └── pipes/             # Validation pipes
├── database/              # Database configuration
├── models/                # Objection.js models
└── templates/             # Email templates
migrations/                # Database migrations
test/                      # Test files
```

## Database Schema

The application uses the following main tables:
- `users` - User accounts and profiles
- `addresses` - User addresses
- `bank_details` - Banking information
- `login_logs` - Authentication attempt logs

## Security Features

- **Password Hashing**: Uses bcrypt for secure password storage
- **JWT Tokens**: Stateless authentication with configurable expiration
- **Role-Based Permissions**: Granular access control
- **Input Validation**: Joi schemas for request validation
- **Rate Limiting**: Throttling to prevent abuse
- **Audit Logging**: Tracks login attempts and account changes

## Contributing

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add some amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

## License

This project is licensed under the UNLICENSED License.
$ pnpm run test

# e2e tests
$ pnpm run test:e2e

# test coverage
$ pnpm run test:cov
```

## Deployment

When you're ready to deploy your NestJS application to production, there are some key steps you can take to ensure it runs as efficiently as possible. Check out the [deployment documentation](https://docs.nestjs.com/deployment) for more information.

If you are looking for a cloud-based platform to deploy your NestJS application, check out [Mau](https://mau.nestjs.com), our official platform for deploying NestJS applications on AWS. Mau makes deployment straightforward and fast, requiring just a few simple steps:

```bash
$ pnpm install -g @nestjs/mau
$ mau deploy
```

With Mau, you can deploy your application in just a few clicks, allowing you to focus on building features rather than managing infrastructure.

## Resources

Check out a few resources that may come in handy when working with NestJS:

- Visit the [NestJS Documentation](https://docs.nestjs.com) to learn more about the framework.
- For questions and support, please visit our [Discord channel](https://discord.gg/G7Qnnhy).
- To dive deeper and get more hands-on experience, check out our official video [courses](https://courses.nestjs.com/).
- Deploy your application to AWS with the help of [NestJS Mau](https://mau.nestjs.com) in just a few clicks.
- Visualize your application graph and interact with the NestJS application in real-time using [NestJS Devtools](https://devtools.nestjs.com).
- Need help with your project (part-time to full-time)? Check out our official [enterprise support](https://enterprise.nestjs.com).
- To stay in the loop and get updates, follow us on [X](https://x.com/nestframework) and [LinkedIn](https://linkedin.com/company/nestjs).
- Looking for a job, or have a job to offer? Check out our official [Jobs board](https://jobs.nestjs.com).

## Support

Nest is an MIT-licensed open source project. It can grow thanks to the sponsors and support by the amazing backers. If you'd like to join them, please [read more here](https://docs.nestjs.com/support).

## Stay in touch

- Author - [Kamil Myśliwiec](https://twitter.com/kammysliwiec)
- Website - [https://nestjs.com](https://nestjs.com/)
- Twitter - [@nestframework](https://twitter.com/nestframework)

## License

Nest is [MIT licensed](https://github.com/nestjs/nest/blob/master/LICENSE).
