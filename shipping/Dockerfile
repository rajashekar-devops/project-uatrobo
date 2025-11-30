FROM maven:3.9 AS builder
WORKDIR /opt/roboshop-shipping
COPY src ./src
COPY pom.xml .
RUN mvn clean package && \
    mv target/*.jar shipping.jar


FROM eclipse-temurin:17-jre-alpine
EXPOSE 8080
WORKDIR /opt/roboshop-shipping
RUN addgroup -S roboshop && adduser -S roboshop -G roboshop
EXPOSE 8080
COPY --from=builder --chown=roboshop:roboshop /opt/roboshop-shipping/shipping.jar .
USER roboshop
ENV CART_ENDPOINT="cart:8080" \
    DB_HOST="mysql"
CMD ["java", "-jar", "shipping.jar"]




# FROM maven:3.9
# EXPOSE 8080
# WORKDIR /opt/roboshop-shipping
# COPY src ./src
# COPY pom.xml .
# RUN mvn clean package
# RUN mv target/*.jar shipping.jar
# ENV CART_ENDPOINT="cart:8080" \
#     DB_HOST="mysql"
# CMD ["java", "-jar", "shipping.jar"]