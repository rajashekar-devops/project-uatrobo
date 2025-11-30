FROM python:3.9.25-alpine3.21 AS build
WORKDIR /opt/roboshop-payment
RUN apk add --no-cache \
    build-base \
    linux-headers \
    pcre-dev
COPY requirements.txt .
RUN pip3 install --prefix=/install -r requirements.txt


FROM python:3.9.25-alpine3.21
EXPOSE 8080
WORKDIR /opt/roboshop-payment
# Install runtime dependencies only
RUN apk add --no-cache pcre
RUN addgroup -S roboshop && adduser -S roboshop -G roboshop
# copy python packages installed from build stage
# COPY --from=build /install /usr/local
COPY --from=build /install /usr/local
COPY --chown=roboshop:roboshop payment.ini *.py requirements.txt .
ENV CART_HOST="cart" \
    CART_PORT="8080" \
    USER_HOST="user" \
    USER_PORT="8080" \
    AMQP_HOST="rabbitmq" \
    AMQP_USER="roboshop" \
    AMQP_PASS="roboshop123"
USER roboshop
CMD ["uwsgi","--ini","payment.ini"]



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