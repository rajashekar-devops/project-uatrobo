FROM node:20.19-alpine AS build
WORKDIR /opt/roboshop-cart
COPY package.json .
COPY *.js .
run npm install



FROM node:20.19-alpine
WORKDIR /opt/roboshop-cart
RUN addgroup -S roboshop && adduser -S roboshop -G roboshop && \
    chown -R roboshop:roboshop /opt/roboshop-cart
EXPOSE 8080
ENV REDIS_HOST="redis" \
    CART_HOST="cart" \
    CART_PORT="8080"
COPY --from=build /opt/roboshop-cart /opt/roboshop-cart

LABEL com.projects="roboshop" \
      component="cart" \
      created_by="rajashekar"
USER roboshop
ENTRYPOINT ["node"]
CMD ["server.js"]







# FROM node:20
# EXPOSE 8080
# WORKDIR /opt/roboshop-cart
# COPY *.js .
# COPY package.json .
# RUN npm install
# ENV REDIS_HOST="redis" \
#     cart_HOST="cart" \
#     cart_PORT="8080"
# CMD ["node","server.js"]