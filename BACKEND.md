# StreamCast - Backend

![NestJS](https://img.shields.io/badge/NestJS-303030?style=flat-square&logo=nestjs&logoColor=E0234E)
![TypeORM](https://img.shields.io/badge/TypeORM-303030?style=flat-square&logo=typeorm&logoColor=FE0803)
![Docker](https://img.shields.io/badge/Docker-303030?style=flat-square&logo=docker&logoColor=2496ED)
![PostgreSQL](https://img.shields.io/badge/PostgreSQL-303030?style=flat-square&logo=postgresql&logoColor=4169E1)
![pnpm](https://img.shields.io/badge/Pnpm-303030?style=flat-square&logo=pnpm&logoColor=F69220)
![swagger](https://img.shields.io/badge/Swagger-303030?style=flat-square&logo=swagger&logoColor=85EA2D)

A robust and scalable backend application for the StreamCast platform, built with NestJS, TypeORM, and PostgreSQL. It provides a RESTful API for managing streaming content and user data.

## Features

- **RESTful API**: Exposes endpoints for managing items (e.g., create, read, update, delete).
- **Database Integration**: Seamlessly connects with PostgreSQL using TypeORM for efficient data management.
- **Modular Structure**: Organized into modules (e.g., `AppModule`, `DatabaseModule`, `ItemsModule`) for better maintainability and scalability.
- **Environment Configuration**: Utilizes `@nestjs/config` and `dotenv` for flexible environment variable management.
- **Docker Support**: Easily set up and run the PostgreSQL database using Docker Compose.
- **Validation**: Implements `class-validator` for robust data validation on DTOs.

## Getting Started

Follow these instructions to set up and run the project locally.

### Prerequisites

Make sure you have the following installed on your system:

- [Node.js](https://nodejs.org/)
- [pnpm](https://pnpm.io/installation)
- [Docker](https://www.docker.com/get-started)

### Installation

1.  Clone the repository:

    ```bash
    git clone https://github.com/your-username/stream-cast-backend.git
    cd stream-cast-backend
    ```

2.  Copy `.env.sample` to `.env` and configure your environment variables:

    ```bash
    cp .env.sample .env
    ```

3.  Start Docker Compose (if needed):

    ```bash
    docker-compose up -d
    ```

4.  Install dependencies:

    ```bash
    pnpm install
    ```

### Running the Development Server

To start the development server (with hot-reloading):

```bash
pnpm run start:dev
```

This will typically run the API on `http://localhost:3030` (or the port specified in your `.env` file).

> Swagger API documentation will be available at `http://localhost:3030/api` and JSON API documentation at `http://localhost:3030/api-json`.

### Running with Docker Compose

To start the PostgreSQL database using Docker Compose:

```bash
docker-compose up -d
```

Then, you can start the NestJS application as usual:

```bash
pnpm run start:dev
```

### Building for Production

To build the application for production:

```bash
pnpm run build
```

This will create a `dist` folder with the optimized production build.

To run the production build:

```bash
pnpm run start:prod
```

### Linting and Formatting

- **Lint and fix issues**:

```bash
pnpm run lint
```

- **Format code**:

```bash
pnpm run format
```

## Project Structure

```bash
.
├── 📁 src/                    # Source code
│   ├── 📁 common/             # Common utilities, constants, and response messages
│   ├── 📁 database/           # Database configuration and TypeORM setup
│   ├── 📁 items/              # Module for item-related logic (controllers, services, entities, DTOs, repositories)
│   │   ├── 📁 constant/
│   │   ├── 📁 controller/
│   │   ├── 📁 dto/
│   │   ├── 📁 entities/
│   │   ├── 📁 repository/
│   │   └── 📁 service/
│   ├── 📄 app.module.ts       # Main application module
│   └── 📄 main.ts             # Application entry point
├── 📁 test/                   # E2E tests
├── ⚙️ .env.sample             # Example environment variables
├── 📄 .gitignore              # Files and directories to ignore in Git
├── ⚙️ .husky/                 # Git hooks configuration
├── ⚙️ .prettierrc             # Prettier configuration
├── ⚙️ commitlint.config.js    # Commitlint configuration
├── 📄 docker-compose.yml      # Docker Compose setup for PostgreSQL
├── ⚙️ eslint.config.mjs       # ESLint configuration
├── ⚙️ nest-cli.json           # NestJS CLI configuration
├── 📄 package.json            # Project dependencies and scripts
├── 📄 pnpm-lock.yaml          # pnpm lock file
├── 📄 README.md               # Project README file
├── ⚙️ tsconfig.build.json     # TypeScript build configuration
└── ⚙️ tsconfig.json           # TypeScript configuration
```

## License

This project is UNLICENSED. Please refer to the `package.json` for more details. (Note: Consider adding a specific license for open-source projects.)