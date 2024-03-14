# Base image
FROM node:14

# Label
LABEL author="Navinkumar Boddu"

ARG buildversion

ENV build=$buildversion

# Set working directory for subsequent commands
WORKDIR /node_app

# Copy app, templates and views
COPY package.json .

# Install dependencies
RUN npm install

# Copy app, templates and views
COPY . .

EXPOSE $PORT

RUN echo "Build version: $build"

# Command to run when container starts
ENTRYPOINT ["npm", "start"]
