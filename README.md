# playground

This repository contains a Quarkus-based microservice and a React TypeScript frontend.

- `backend` - Quarkus REST API exposing `/api/hello`.
- `frontend` - React application that fetches the greeting from the backend.

## Development

### Backend

```bash
cd backend
mvn quarkus:dev
```

### Frontend

```bash
cd frontend
npm install
npm run dev
```
