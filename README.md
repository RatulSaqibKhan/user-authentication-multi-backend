# **Authentication Framework Showcase**

This repository demonstrates user authentication implementations using various backend frameworks. Each framework is containerized using Docker for a consistent development environment. The goal is to provide working examples for common authentication methods like JWT, OAuth2, and Session-based authentication in popular backend technologies.

## **Project Structure**

```
apps/
│
├── frameworks/            # Backend frameworks for authentication
│   ├── express/           # Node.js + Express framework
│   ├── nestjs/            # NestJS framework
│   ├── django/            # Django framework
│   ├── flask/             # Flask framework
│   ├── laravel/           # Laravel framework
│   └── springboot/        # Spring Boot framework
│
├── docker/                # Docker setup for each framework
│   ├── .envs/             # Environment files
│   ├── express/           # Docker for Express
│   ├── nestjs/            # Docker for NestJS
│   ├── django/            # Docker for Django
│   ├── flask/             # Docker for Flask
│   ├── laravel/           # Docker for Laravel
│   ├── springboot/        # Docker for Spring Boot
│   ├── .env.example       # Example environment variables
│   ├── docker.compose.override.yml.example
│   └── docker-compose.yml # Main Docker Compose file for running the project
│
├── README.md              # Project documentation
├── docker-compose.yml     # Docker Compose file to orchestrate services
└── .gitignore             # Ignore files for version control
```
## Authentication Implementations

This repository includes examples of basic user authentication for various web frameworks. Each framework demonstrates multiple authentication strategies, such as:

- **JWT Authentication**
- **Session-based Authentication**
- **OAuth2 Authentication**

## Frameworks To Be Covered

- **Express (Node.js)**
- **NestJS (Node.js)**
- **Django (Python)**
- **Flask (Python)**
- **Laravel (PHP)**
- **Spring Boot (Java)**

Each framework is located in the `/frameworks` directory and contains its own `README.md` file with specific setup instructions and details about the authentication flow.

