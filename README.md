# Global Loyalty Indonesia Academy Spring Boot Microservices Project

## Table of Contents
- [Introduction](#introduction)
- [Architecture Overview](#architecture-overview)
- [Services](#services)
  - [User Management Service](#user-management-service)
  - [Asteroid Data Service](#asteroid-data-service)
- [Technologies Used](#technologies-used)
- [Installation](#installation)

## Introduction
This project is composed of two microservices:
1. **User Management Service**: Handles user authentication and authorization using Redis for session management and JWT tokens.
2. **Asteroid Data Service**: Fetches asteroid data from NASA's public API and performs CRUD operations on it using PostgreSQL. Access to this service is controlled through authentication from the User Management Service.

## Architecture Overview
- **Microservices**: Two independent services communicating via REST API.
- **Authentication & Authorization**: JWT-based token authentication managed by Redis.
- **Persistence**: User sessions are stored in Redis, and asteroid data is stored in PostgreSQL.
- **External API Integration**: Asteroid data is fetched from NASA's NeoWs API.

## Services

### User Management Service
This service is responsible for:
- User registration and login.
- Authentication via JWT.
- Storing user sessions in Redis.
- Verifying token validity when accessing other services.

#### Endpoints
- `POST /auth/register` - Register a new user.
- `POST /auth/login` - Login and receive JWT token.
- `POST /auth/login` - Refresh JWT token if token expired.
- `POST /auth/validate` - Verify the validity of a JWT token (used by the `Asteroid Data Service`).

### Asteroid Data Service
This service handles:
- Fetching asteroid data from NASA's NeoWs API.
- Storing fetched data into PostgreSQL.
- Performing CRUD operations on asteroid data (create, read, update, delete).
- Validating user tokens by calling the User Management Service.

#### Endpoints
- `GET /asteroid` - Get all stored asteroids (requires authentication).
- `GET /asteroid/{id}` - Get specific asteroid by ID (requires authentication).
- `POST /save` - Fetch and store asteroid data from NASA (requires authentication).
- `PUT /asteroid/{id}` - Update specific asteroid data (requires authentication).
- `DELETE /asteroid/{id}` - Delete asteroid by ID (requires authentication).

## Technologies Used
- **Spring Boot**: Core framework for developing both services.
- **Redis**: For storing user data in `User Management Service`.
- **PostgreSQL**: For storing asteroid data in `Asteroid Data Service`.
- **Docker**: Used to run Redis, PostgreSQL, and both services containers.
- **NASA NeoWs API**: External API for fetching asteroid data.
- **JWT**: Token-based authentication.

## Installation
### Prerequisites
- Docker installed on your system.
- Java 17+ and Maven.
