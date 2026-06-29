FROM node:10 AS ui-build
WORKDIR /usr/src/app
COPY my-app/ ./my-app/
RUN cd my-app && npm install && npm run build

FROM node:10 AS server-build
WORKDIR /root/
COPY --from=ui-build /usr/src/app/my-app/build ./my-app/build
COPY api/package*.json ./api/
RUN cd api && npm install
COPY api/server.js ./api/

RUN groupadd --gid 1000 nodejs && \
    useradd --uid 1000 --gid nodejs --shell /bin/bash --no-create-home nodejs

USER nodejs

EXPOSE 3080

CMD ["node", "./api/server.js"]
