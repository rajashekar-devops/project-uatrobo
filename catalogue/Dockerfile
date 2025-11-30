FROM node:20.19-alpine AS build
WORKDIR /opt/roboshop-catalogue
COPY package.json .
COPY *.js .
run npm install



FROM node:20.19-alpine
WORKDIR /opt/roboshop-catalogue
USER roboshop
COPY --from=build /opt/roboshop-catalogue /opt/roboshop-catalogue
ENV MONGO="true" \
    MONGO_URL="mongodb://mongodb:27017/catalogue"
RUN chown -R roboshop:roboshop /opt/roboshop-catalogue
CMD ["node","server.js"]








# FROM node:20
# WORKDIR /opt/roboshop-catalogue
# COPY package.json .
# COPY *.js .
# run npm install
# ENV MONGO="true" \
#     MONGO_URL="mongodb://mongodb:27017/catalogue"
# CMD ["node","server.js"]