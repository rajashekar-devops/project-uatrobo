FROM node:20
WORKDIR /opt/roboshop-catalogue
COPY package.json .
COPY *.js .
run npm install
ENV MONGO="true" \
    MONGO_URL="mongodb://mongodb:27017/catalogue"
CMD ["node","server.js"]