FROM node:lts-alpine
WORKDIR /app
COPY ./dist/apps/svc-cart .
ENV PORT=3336
EXPOSE ${PORT}
RUN npm install --production
# dependencies that express needs
RUN npm install reflect-metadata tslib rxjs express
CMD node ./main.js
