FROM node:20-alpine

WORKDIR /app

# Install dependencies
COPY package*.json ./
RUN npm config set fetch-retries 5 && \
    npm config set fetch-retry-mintimeout 20000 && \
    npm config set fetch-retry-maxtimeout 120000 && \
    npm ci --omit=dev --no-audit --no-fund && \
    test -f node_modules/express/package.json

# Copy application source
COPY server.js ./
COPY public ./public/

# Make the app directory accessible to OpenShift's arbitrarily assigned
# non-root UID (which always belongs to group 0 / root group)
RUN chgrp -R 0 /app && chmod -R g=u /app

EXPOSE 3000
CMD ["node", "server.js"]
