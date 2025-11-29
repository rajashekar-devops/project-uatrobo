FROM maven:3.9
EXPOSE 8080
WORKDIR /opt/roboshop-shipping
COPY src ./src
COPY pom.xml .
RUN mvn clean package
COPY target/*.jar shipping.jar
ENV CART_ENDPOINT="cart:8080" \
    DB_HOST="mysql"
CMD ["java", "-jar", "shipping.jar"]