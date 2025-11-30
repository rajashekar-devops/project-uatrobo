FROM node:20.19-alpine AS build
WORKDIR /opt/roboshop-user
COPY package.json .
COPY *.js .
run npm install



FROM node:20.19-alpine
WORKDIR /opt/roboshop-user
RUN addgroup -S roboshop && adduser -S roboshop -G roboshop && \
    chown -R roboshop:roboshop /opt/roboshop-user
EXPOSE 8080
ENV MONGO="true" \
    REDIS_URL='redis://redis:6379' \
    MONGO_URL="mongodb://mongodb:27017/users"
COPY --from=build /opt/roboshop-user /opt/roboshop-user
LABEL com.projects="roboshop" \
      component="user" \
      created_by="rajashekar"
USER roboshop
ENTRYPOINT ["node"]
CMD ["server.js"]




# FROM node:20
# EXPOSE 8080
# WORKDIR /opt/roboshop-user
# COPY *.js .
# COPY package.json .
# RUN npm install
# ENV MONGO="true" \
#     REDIS_URL='redis://redis:6379' \
#     MONGO_URL="mongodb://mongodb:27017/users"
# CMD ["node","server.js"]