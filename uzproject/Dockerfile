FROM node:20-alpine
WORKDIR /app
COPY package*.json ./
RUN npm install --omit=dev
COPY . .
ENV HOST=0.0.0.0 PORT=3000
EXPOSE 3000
CMD node index.js
