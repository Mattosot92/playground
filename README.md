# playground

This repository contains a Quarkus-based microservice and an embedded React TypeScript frontend.

- `backend` - Quarkus REST API exposing `/api/hello`.
- `backend/src/main/frontend` - React application that fetches the greeting from the backend.

## Development

### Backend

```bash
cd backend
mvn quarkus:dev
```

### Frontend (HMR Dev)

```bash
cd backend/src/main/frontend
npm install
npm run dev
```

## Serve Frontend From Backend

The backend now serves the built frontend directly, so the React UI is available at the backend root.

- Build the frontend into Quarkus' static resources:
  - `npm --prefix backend/src/main/frontend run build`

- Run the backend (serves UI at `/` and API at `/api`):
  - `mvn -f backend quarkus:dev`
  - Open `http://localhost:8080`

Notes:
- The Vite dev server still works for HMR during development and proxies `/api` to `http://localhost:8080`.
- Production builds output to `backend/src/main/resources/META-INF/resources` and are served by Quarkus automatically.

## Maven Integration

The Maven build runs the frontend build automatically using `frontend-maven-plugin`:

- Package everything (runs `npm install` and `npm run build` in `backend/src/main/frontend`):
  - `mvn -f backend package`

- Skip the frontend during Maven builds if needed:
  - `mvn -f backend package -DskipFrontend=true`

Notes:
- The plugin downloads and uses a local Node.js/npm for reproducible builds.
