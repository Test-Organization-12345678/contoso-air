# --- Build stage ---
FROM node:22 AS builder
RUN mkdir -p /usr/src/app
WORKDIR /usr/src/app
COPY package*.json .
RUN npm ci
COPY . .
RUN npm run build          # ← build happens HERE, at image build time

# --- Runtime stage ---
FROM node:22
WORKDIR /usr/src/app
COPY --from=builder /usr/src/app .
COPY --from=builder /usr/src/app/.next .next
ENV PORT 3000
EXPOSE 3000

CMD ["npx", "next", "start"]
