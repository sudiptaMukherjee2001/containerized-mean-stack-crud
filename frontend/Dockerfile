# ---------- Stage 1: Install Dependencies ----------
FROM node:20-alpine AS builder

WORKDIR /frontend

# Copy only package files first (better caching)
COPY package*.json ./

# Install production dependencies only
RUN npm ci --omit=dev

# Copy remaining source code
COPY . .


# ---------- Stage 2: Runtime Image ----------
FROM node:20-alpine

WORKDIR /frontend

# Copy only necessary files from builder
COPY --from=builder /frontend /frontend

EXPOSE 4200

CMD ["npx", "ng", "serve", "--host", "0.0.0.0", "--port", "4200"]