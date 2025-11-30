FROM node:20.19-alpine AS build
WORKDIR /opt/roboshop-catalogue
COPY package.json .
COPY *.js .
run npm install



FROM node:20.19-alpine
WORKDIR /opt/roboshop-catalogue
RUN addgroup -S roboshop && adduser -S roboshop -G roboshop && \
    chown -R roboshop:roboshop /opt/roboshop-catalogue
ENV MONGO="true" \
    MONGO_URL="mongodb://mongodb:27017/catalogue"
COPY --from=build /opt/roboshop-catalogue /opt/roboshop-catalogue
EXPOSE 8080
LABEL com.projects="roboshop" \
      component="catalogue" \
      created_by="rajashekar"
USER roboshop
ENTRYPOINT ["node"]
CMD ["server.js"]








# FROM node:20
# WORKDIR /opt/roboshop-catalogue
# COPY package.json .
# COPY *.js .
# run npm install
# ENV MONGO="true" \
#     MONGO_URL="mongodb://mongodb:27017/catalogue"
# CMD ["node","server.js"]