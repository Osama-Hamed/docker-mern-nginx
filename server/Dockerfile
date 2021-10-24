FROM node:14.18.1-alpine
WORKDIR /app
COPY package.json .
RUN yarn
COPY . .
EXPOSE 4000
CMD yarn start
