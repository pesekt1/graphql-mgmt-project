# GraphQL demo - management system

A full-stack project management system demo using GraphQL, Node.js, Express, MongoDB, and a React client. The project is containerized using Docker Compose for easy setup and development. It demonstrates how to build and connect a GraphQL API with a modern client and database, supporting CRUD operations for projects and clients.

- **Docker Compose:**

  - Builds and runs three services: server, client, and MongoDB.
  - Volumes are mounted for live code updates.

## Getting Started

1. **Install Docker and Docker Compose** if you haven't already.

2. **Start all services** (server, client, and database) from the project root:

   ```bash
   docker-compose up --build
   ```

   - **GraphQL server:** [http://localhost:5001/graphql](http://localhost:5001/graphql)
   - **Client app:** [http://localhost:3001/](http://localhost:3001/)
   - **MongoDB (internal):** `mongodb://db:27017/projectMgmt`

### Ports

- **Server:** `5001` (host) → `5000` (container)
- **Client:** `3001` (host) → `3000` (container)
- **MongoDB:** `27018` (host) → `27017` (container)

## Server

### Usage

- Access the GraphQL playground at `http://localhost:5001/graphql` (when `NODE_ENV=development`).
- Use GraphQL queries and mutations to manage projects and clients.

### Server details

- **Tech stack:** Node.js, Express, GraphQL, MongoDB (via Mongoose)
- **Entry point:** `project-mgmt-graphql-server/index.js`
- **GraphQL endpoint:** `/graphql`
- **Environment variables:**

  - `MONGO_URI` (MongoDB connection string, set automatically in Docker Compose)
  - `PORT` (default: 5000, mapped to 5001 on host)
  - `NODE_ENV` (set to `development` for GraphiQL playground)

- **Schema:**

  - Projects and Clients are the main types.
  - Projects reference Clients via `clientId`.
  - Supports queries and mutations for CRUD operations on both Projects and Clients.

- **Database:**

  - Uses MongoDB, with data persisted in a Docker volume (`mongodb_data`).
  - Example data can be found in `project-mgmt-graphql-server/data/clients.json`.

  - **Development:**

  - Hot-reloading enabled via `nodemon` in development mode.
  - CORS enabled for API access.

## Client

### Usage

- Access the client app at `http://localhost:3001/` in your browser.
- Use the UI to view, add, edit, and delete projects and clients.
- The client communicates with the GraphQL API at `http://localhost:5001/graphql`.

### Client details

- **Tech stack:** React, Apollo Client, React Router
- **Entry point:** `project-mgmt-client/src/App.js`
- **GraphQL endpoint:** Configured to `http://localhost:5001/graphql` via Apollo Client
- **Features:**
  - List, add, edit, and delete projects and clients
  - View project details, including associated client info
  - Responsive UI with modals for adding/editing
  - Uses Apollo Client for GraphQL queries and mutations
- **Development:**
  - Hot-reloading enabled via Create React App
  - All dependencies managed in `project-mgmt-client/package.json`
  - Code splitting and routing handled by React Router
