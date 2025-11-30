FROM python:3.11-alpine AS build
RUN apk add --no-cache \
    build-base \
    linux-headers \
    pcre-dev \
    python3-dev
WORKDIR /opt/roboshop-payment
COPY payment.ini .
COPY *.py .
COPY requirements.txt .
RUN pip3 install -r requirements.txt


FROM python:3.11-alpine
EXPOSE 8080
WORKDIR /opt/roboshop-payment
RUN addgroup -S roboshop && adduser -S roboshop -G roboshop
COPY --from=build --chown=roboshop:roboshop /opt/roboshop-payment/ .
USER roboshop
ENV CART_HOST="cart" \
    CART_PORT="8080" \
    USER_HOST="user" \
    USER_PORT="8080" \
    AMQP_HOST="rabbitmq" \
    AMQP_USER="roboshop" \
    AMQP_PASS="roboshop123"
CMD ["uwsgi", "--ini", "payment.ini"]



# FROM python:3.9
# EXPOSE 8080
# WORKDIR /opt/roboshop-payment
# COPY payment.ini .
# COPY *.py .
# COPY requirements.txt .
# RUN pip3 install -r requirements.txt
# ENV CART_HOST="cart" \
#     CART_PORT="8080" \
#     USER_HOST="user" \
#     USER_PORT="8080" \
#     AMQP_HOST="rabbitmq" \
#     AMQP_USER="roboshop" \
#     AMQP_PASS="roboshop123"
# CMD ["uwsgi", "--ini", "payment.ini"]