# Backend Course Documentation

Step-by-step backend development notes, code snippets, and practical references from working through **[Backend Full Course | NodeJS ExpressJS PostgreSQL Prisma & Docker](https://www.youtube.com/watch?v=9BD9eK9VqXA)** by [Smoljames](https://www.youtube.com/@smoljames).

I'm documenting this course as I expand my backend development skills and transition toward full-stack development (frontend-focused). These notes are intended to be a practical reference for future projects, troubleshooting, and teaching.

## Course Overview

The course introduces backend development through progressively more complex projects using JavaScript, Node.js, Express, databases, authentication, and Docker.

The four chapters build on the same core concepts, moving from a basic HTTP server to a containerized full-stack application.

### Chapter 1 — Backend Fundamentals

An introduction to the technologies and communication patterns that make full-stack applications work.

**Topics covered:**

- Frontend vs. backend development
- Clients, servers, and networks
- URLs, IP addresses, and DNS
- HTTP requests and responses
- How a browser communicates with a backend server

This chapter provides the conceptual foundation for the hands-on projects.

### Chapter 2 — Building an Express Server

Build a basic HTTP server using Node.js and Express.

**Topics covered:**

- Creating and initializing a Node.js project
- Working with npm and `package.json`
- Installing Express and nodemon
- Creating and running a server
- HTTP methods, routes, and endpoints
- Website endpoints vs. API endpoints
- CRUD operations
- Middleware and JSON request bodies
- Testing HTTP requests using the VS Code REST Client

**Project:** A simple Express server that serves HTML pages and supports basic API requests.

[Chapter 2 Documentation](chapter_2/README.md)

### Chapter 3 — Building a Full-Stack Application

Expand the introductory server into an authenticated application with persistent data storage.

**Topics covered:**

- Organizing a larger Node.js project
- Working with SQLite
- Creating database tables and queries
- Serving frontend files
- Structuring API routes
- User registration and authentication
- Password handling and protected routes
- Creating, reading, updating, and deleting database records

**Project:** An authenticated to-do application backed by SQLite.

_Detailed documentation to be added._

### Chapter 4 — PostgreSQL, Prisma, and Docker

Build on the Chapter 3 application using additional tools for database management and containerization.

**Topics covered:**

- PostgreSQL
- Object-relational mapping (ORM)
- Prisma schemas and database operations
- Database migrations
- Docker containers
- Docker Compose
- Connecting an application to a separate database service
- Running a containerized full-stack application

**Project:** An updated version of the to-do application using PostgreSQL, Prisma, and Docker.

_Detailed documentation to be added._

## Technologies

| Technology          | Purpose                                      |
| ------------------- | -------------------------------------------- |
| Node.js             | JavaScript runtime for the backend           |
| Express             | HTTP server and routing framework            |
| npm                 | Package and dependency management            |
| nodemon             | Automatic server restarts during development |
| SQLite              | Lightweight relational database              |
| PostgreSQL          | Relational database                          |
| Prisma              | Object-relational mapper                     |
| Docker              | Application containerization                 |
| Docker Compose      | Managing multiple application services       |
| VS Code REST Client | Testing HTTP requests                        |

## Using This Documentation

Each chapter contains a practical development guide with:

1. **Steps** — Commands and code snippets needed to implement each feature.
2. **Concepts** — Brief explanations of important technical concepts.
3. **Verification** — How to confirm that the implementation works.
4. **Notes** — Observations, troubleshooting tips, and important reminders.

The goal is to make these documents useful independently of the original tutorial, while providing links back to the source for additional explanations and demonstrations.

## Attribution and Acknowledgments

This project was developed while following the excellent [Backend Full Course by Smoljames](https://www.youtube.com/watch?v=9BD9eK9VqXA).

I worked through the video, wrote and tested the code, and took notes on the concepts and explanations I found particularly helpful.

These documents organize that learning into step-by-step development references, with additional explanations, modifications, and corrections where appropriate.

Full credit to James for creating the original tutorial and providing such a clear introduction to backend development.

**I highly recommend watching the original course for the complete explanations and demonstrations.**

This repository contains independent learning notes and is not an official reproduction of, or replacement for, the original course.
