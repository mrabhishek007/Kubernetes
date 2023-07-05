FROM node:14

WORKDIR /app

COPY package.json .

RUN npm install

COPY . .

ARG DEFAULT_PORT=80

ENV PORT $DEFAULT_PORT

EXPOSE $PORT


# VOLUME ["/app/feedback] # Anonymous Volume Will get destroyed once container destroyed. Use Named volume for data presistency
# VOLUME [ "/app/node_modules" ] # Can be used when bind mount is used . It will give more preference to the node moudles of container instead on the host machine node modules

CMD [ "npm", "start" ]