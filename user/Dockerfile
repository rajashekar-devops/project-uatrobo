FROM node:20
EXPOSE 8080
WORKDIR /opt/roboshop-user
COPY *.js .
COPY package.json .
RUN npm install
ENV MONGO="true" \
    REDIS_URL='redis://redis:6379' \
    MONGO_URL="mongodb://mongodb:27017/users"
CMD ["node","server.js"]