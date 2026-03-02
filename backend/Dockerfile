FROM node:lts-alpine

# Create app directory
WORKDIR /usr/src/app

#COPY THE DEPENDENCIES FILES
COPY package*.json ./

# INSTALL THE DEPENDENCIES . ci is used to install the exact versions of dependencies as specified in package-lock.json
RUN npm ci --only=production

#COPY THE SOURCE CODE
COPY . .
#EXPOSE THE PORT
EXPOSE 8081

#START THE APPLICATION
CMD ["node", "server.js"]