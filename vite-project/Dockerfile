FROM node:20-alpine

# 1. Create the user and group
RUN addgroup app && adduser -S -G app app

# 2. Set the working directory
WORKDIR /app

# 3. Copy package files
COPY package*.json ./

# 4. Fix permissions for BOTH the app directory AND the user's home directory
# This ensures npm has a place to put its cache.
RUN mkdir -p /home/app/.npm && \
    chown -R app:app /home/app && \
    chown -R app:app /app

# 5. Switch to the non-root user
USER app

# 6. Install dependencies
RUN npm install

# 7. Copy the rest of the source code
COPY --chown=app:app . .

EXPOSE 5173

CMD ["npm", "run", "dev"]