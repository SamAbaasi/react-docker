# ⚡ Vite + React + TypeScript + Docker Starter

This project is a **production-ready React app** built with **Vite**, **TypeScript**, and **Docker**, following industry best practices:

- 🔐 Multi-stage Docker builds for smaller, secure images  
- ⚙️ TypeScript + ESLint integration  
- 🧱 Minimal and clean project setup  
- 🌐 Production server using **Nginx**  
- 🚀 CI/CD and container-friendly  

---

## 📦 Tech Stack

- [React](https://reactjs.org/)
- [Vite](https://vitejs.dev/)
- [TypeScript](https://www.typescriptlang.org/)
- [Docker](https://www.docker.com/)
- [Nginx](https://nginx.org/)

---

## 📁 Project Structure

vite-react-ts-app/
├── public/
│ └── favicon.svg
├── src/
│ ├── App.tsx
│ ├── main.tsx
│ └── vite-env.d.ts
├── .dockerignore
├── Dockerfile
├── index.html
├── package.json
├── tsconfig.json
├── vite.config.ts
└── package-lock.json


---

## 🚀 Scripts


---

## 🚀 Scripts

| Script             | Description                            |
|--------------------|----------------------------------------|
| `npm run dev`      | Run local dev server (Vite)            |
| `npm run build`    | Build for production                   |
| `npm run preview`  | Preview built app (Vite static server) |
| `npm run lint`     | Run ESLint                             |
| `npm run type-check` | Run TypeScript without emitting files |

---

## 🐳 Docker Instructions

### 🔨 Build the Image

```bash
docker build -t react-docker .
```

###  ▶️ Run the Container
```bash
docker run -p 3000:80 react-docker
Visit: http://localhost:3000
```
### 🔁 Multi-Stage Dockerfile Breakdown
Dockerfile
```bash
# Stage 1: Build
FROM node:20-alpine AS builder

WORKDIR /app

COPY package*.json ./
RUN npm ci

COPY . .
RUN npm run build

# Stage 2: Serve with Nginx
FROM nginx:stable-alpine as production

# Copy build output to Nginx's web directory
COPY --from=builder /app/dist /usr/share/nginx/html

# Replace default nginx config (optional)
COPY nginx.conf /etc/nginx/conf.d/default.conf

EXPOSE 80

# Start nginx
CMD ["nginx", "-g", "daemon off;"]

```
### 📁 .dockerignore
```bash
node_modules
dist
.git
Dockerfile
docker-compose.yml
.env
```
###  ✅ Best Practices Implemented
✅ Multi-stage builds for optimized final image

✅ Alpine base images: node:20-alpine, nginx:stable-alpine

✅ .dockerignore to reduce context size

✅ No secrets included in Docker image

✅ Deterministic installs via npm ci

✅ Version-pinned base images

✅ Clean build artifacts and minimal layers

✅ Default port 80 exposed for Nginx



