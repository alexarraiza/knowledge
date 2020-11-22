# Development environments

## Typescript

### Typescript - node+express

- You need all the `.env` files on a folder called `env` at the root of the project
- The source code must be on a folder called `src`
- You need a `dockerfile.dev` that build the project in dev form

#### dockerfile.dev - node+express

```dockerfile
# base image, change it for the one your project needs
FROM node:10-alpine

# set working directory
WORKDIR /src/app

# setup the linux packages you need
RUN apk --no-cache add --virtual native-deps \
    g++ gcc libgcc libstdc++ linux-headers autoconf automake make nasm python git && \
    npm install --quiet node-gyp -g

# install app dependencies
COPY package.json ./
COPY package-lock.json ./
COPY yarn.lock ./
RUN npm install

# add app
COPY ./src/ ./src/
RUN npm install

# make the port the app uses visible accessible
EXPOSE 8080
CMD ["npm", "run", "start"]
```

#### docker-compose - node+express

```yaml
version: "3.8"
services:
  node:
    build:
      context: .
      dockerfile: dockerfile.dev
    ports:
      - "8080:8080"
    volumes:
      - ./src:/app/src
      - ./node_modules:/app/node_modules
      - ./env:/app/env
    command: ["npm", "run", "start:dev"]
```

### Typescript - react

- You need all the `.env` files on a folder called `env` at the root of the project
- The source code must be on a folder called `src`
- You need a `dockerfile.dev` that build the project in dev form

#### dockerfile.dev - react

```dockerfile
# base image, change it for the one your project needs
FROM node:10-alpine

# set working directory
WORKDIR /app

# add `/app/node_modules/.bin` to $PATH
ENV PATH /app/node_modules/.bin:$PATH

# install app dependencies
COPY package.json ./
COPY package-lock.json ./
COPY yarn.lock ./
RUN npm install
RUN npm install react-scripts@3.4.3 -g

# add app
COPY ./src/ ./src/

# make the port the app uses visible accessible
EXPOSE 3000
# start app
CMD ["npm", "run" , "start:localhost"]
```

#### docker-compose - react

```yaml
version: "3.8"
services:
  react:
    build:
      context: .
      dockerfile: dockerfile.dev
    ports:
      - "3000:3000"
    volumes:
      - ./src:/app/src
      - ./node_modules:/app/node_modules
      - ./env:/app/env
    command: ["npm", "run", "start:dev"]
    environment:
      - CHOKIDAR_USEPOLLING=true
    tty: true
```
