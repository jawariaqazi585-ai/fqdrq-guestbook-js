FROM node:20-alpine

WORKDIR /app

# Install dependencies
COPY package*.json ./
RUN npm install --production

# Copy application source
COPY server.js ./
COPY public ./public/

# Make the app directory accessible to OpenShift's arbitrarily assigned
# non-root UID (which always belongs to group 0 / root group)
RUN chgrp -R 0 /app && chmod -R g=u /app

EXPOSE 3000
CMD ["node", "server.js"]
