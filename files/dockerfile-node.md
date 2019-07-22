<h1 class="title" style="display:none">Dockerfile Node.js</h1>

```
FROM node:10

ARG environment

COPY [".", "/usr/src/"]

WORKDIR /usr/src

ENV NODE_ENV=$environment

RUN chmod 400 jwt.key

RUN npm install

RUN echo "node environment is" $NODE_ENV

EXPOSE 8080

CMD ["node", "index.js"]

```