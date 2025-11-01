FROM node:20-alpine AS builder
WORKDIR /app

# Install deps (including devDependencies for tsc)
COPY package*.json ./
COPY tsconfig.json ./
RUN npm ci

COPY . .

# Compile TypeScript to /app/dist
RUN npx tsc -p tsconfig.json

FROM node:20-alpine AS runner
WORKDIR /app

# Only production dependencies
COPY --from=builder /app/package*.json ./
COPY --from=builder /app/dist ./dist
RUN npm ci --only=production

EXPOSE 3000
CMD ["node", "dist/index.js"]
