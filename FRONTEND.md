# StreamCast - Frontend

![Bun](https://img.shields.io/badge/Bun-232323?style=for-the-badge&logo=bun&logoColor=FFFFFF)
![React](https://img.shields.io/badge/React-232323?style=for-the-badge&logo=react&logoColor=61DAFB)
![TypeScript](https://img.shields.io/badge/TypeScript-232323?style=for-the-badge&logo=typescript&logoColor=3178C6)
![Vite](https://img.shields.io/badge/Vite-232323?style=for-the-badge&logo=vite&logoColor=646CFF)
![Framer Motion](https://img.shields.io/badge/Framer_Motion-232323?style=for-the-badge&logo=framer&logoColor=0055FF)
![Tailwind-CSS](https://img.shields.io/badge/Tailwind_CSS-232323?style=for-the-badge&logo=tailwind-css&logoColor=06B6D4)
![HeroUI](https://img.shields.io/badge/HeroUI-232323?style=for-the-badge&logo=heroui&logoColor=FFFFFF)
![React-Router](https://img.shields.io/badge/React_Router-232323?style=for-the-badge&logo=react-router&logoColor=CA4245)
![Biome](https://img.shields.io/badge/Biome-232323?style=for-the-badge&logo=biome&logoColor=60A5FA)

A modern and responsive web application for streaming and casting content, built with cutting-edge frontend technologies. This project aims to provide a seamless user experience for content consumption and interaction.

## Features

- **Responsive Design**: Adapts to various screen sizes for optimal viewing on desktop, tablet, and mobile.
- **Dynamic Routing**: Utilizes React Router DOM for smooth navigation between different sections of the application.
- **Theme Switching**: Supports light and dark modes for personalized user experience.
- **Component-Based UI**: Built with reusable components using HeroUI and Tailwind CSS for consistent and efficient development.
- **Commit Linting**: Enforces conventional commit messages for a clean and understandable commit history.

## Getting Started

Follow these instructions to set up and run the project locally.

### Prerequisites

Make sure you have [Bun](https://bun.sh/docs/installation) installed on your system.

### Installation

1.  Clone the repository:

    ```bash
    git clone https://github.com/your-username/stream-cast-frontend.git
    cd stream-cast-frontend
    ```

2.  Install dependencies:
    ```bash
    bun install
    ```
3.  Copy `.env.example` to `.env`:
    ```bash
    cp .env.example .env
    ```

### Running the Development Server

To start the development server:

```bash
bun run dev
```

This will typically run the app on `http://localhost:5173`.

### Building for Production

To build the application for production:

```bash
bun run build
```

This will create a `dist` folder with the optimized production build.

### Linting and Formatting

- **Linting**:
  ```bash
  bun run lint
  ```
- **Format Check**:
  ```bash
  bun run format-check
  ```
- **Format and Fix**:
  ```bash
  bun run format
  ```

## Project Structure

```bash
.
├── 📁 public/                 # Static assets
├── 📁 src/
│   ├── 📁 assets/             # Images, fonts, etc.
│   ├── 📁 components/         # Reusable UI components
│   │   ├── 📄 icons.tsx       # SVG icons
│   │   ├── 📄 navbar.tsx      # Navigation bar component
│   │   ├── 📄 primitives.ts   # Tailwind-variants definitions for common styles
│   │   └── 📄 theme-switch.tsx# Theme toggle component
│   ├── 📁 config/             # Application configuration
│   │   └── 📄 site.ts         # Site-specific data (navigation, links)
│   ├── 📁 layouts/            # Layout components (e.g., default layout)
│   │   └── 📄 default.tsx
│   ├── 📁 pages/              # Page components (e.g., index, about, docs)
│   │   ├── 📄 about.tsx
│   │   ├── 📄 blog.tsx
│   │   ├── 📄 docs.tsx
│   │   ├── 📄 index.tsx
│   │   └── 📄 pricing.tsx
│   ├── 📁 styles/             # Global styles
│   │   └── 📄 globals.css
│   ├── 📁 types/              # TypeScript type definitions
│   │   └── 📄 index.ts
│   ├── 📄 App.tsx             # Main application component with routing
│   ├── 📄 main.tsx            # Entry point for React application
│   └── 📄 provider.tsx        # HeroUI provider for context
├── ⚙️ .husky/                 # Git hooks configuration
├── ⚙️ .github/                # GitHub specific configurations (e.g., workflows)
├── 📄 .gitignore              # Files and directories to ignore in Git
├── ⚙️ biome.json              # Biome linter and formatter configuration
├── 📄 bun.lockb               # Bun lock file
├── ⚙️ commitlint.config.js    # Commitlint configuration
├── ⚙️ eslint.config.mjs       # ESLint configuration
├── 📄 index.html              # Main HTML file
├── 📄 package.json            # Project dependencies and scripts
├── ⚙️ postcss.config.js       # PostCSS configuration
├── 📄 README.md               # Project README file
├── ⚙️ tailwind.config.js      # Tailwind CSS configuration
├── ⚙️ tsconfig.json           # TypeScript configuration
├── ⚙️ tsconfig.node.json      # TypeScript configuration for Node.js environment
└── ⚙️ vite.config.ts          # Vite build tool configuration
```

## License

Licensed under the [MIT license](https://github.com/frontio-ai/vite-template/blob/main/LICENSE).