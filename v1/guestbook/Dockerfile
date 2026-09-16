FROM node:20-alpine

WORKDIR /app

# Copy pre-installed dependencies (run `npm install` on the host before building)
COPY node_modules ./node_modules
COPY package*.json ./

# Copy application source
COPY server.js ./
COPY public ./public/

# Make the app directory accessible to OpenShift's arbitrarily assigned
# non-root UID (which always belongs to group 0 / root group)
RUN chgrp -R 0 /app && chmod -R g=u /app

EXPOSE 3000
CMD ["node", "server.js"]
