# Base image
FROM node:alpine

# Label
LABEL author="Navinkumar Boddu"

# ENV
ENV NODE_ENV=production
ENV PORT=3000

# Set working directory for subsequent commands
WORKDIR /var/www

# Copy app, templates and views
COPY package.json package-lock.json ./

# Install dependencies
RUN npm install

# Copy app, templates and views
COPY . ./

EXPOSE $PORT

# Command to run when container starts
ENTRYPOINT ["npm", "start"]
