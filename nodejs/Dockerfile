# FROM mhart/alpine-node-base
# FROM mhart/alpine-node-base:0.10
# FROM mhart/alpine-iojs-base
# FROM mhart/alpine-iojs
FROM mhart/alpine-node:latest

WORKDIR /app

# If you have native dependencies, you'll need extra tools
# RUN apk-install make gcc g++ python

# If you need npm, use mhart/alpine-node or mhart/alpine-iojs
# RUN npm install

# If you had native dependencies you can now remove build tools
# RUN apk del make gcc g++ python && \
#   rm -rf /tmp/* /root/.npm /root/.node-gyp

ENV NODE_ENV production

CMD ["npm", "start"]
