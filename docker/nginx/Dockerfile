FROM nginx:1.19

ENV TZ=UTC

# 將自定義的 Nginx 設定檔複製到容器中
RUN rm -rf /etc/nginx/conf.d/default.conf
COPY ./nginx.conf /etc/nginx/nginx.conf
COPY ./conf.d /etc/nginx/conf.d

RUN mkdir /etc/nginx/global
COPY ./global/*.conf /etc/nginx/global/

COPY ./ssl/certificate.crt /etc/nginx/ssl/certificate.crt
COPY ./ssl/private.key /etc/nginx/ssl/private.key

# 建立 Nginx 日誌檔案
RUN touch /var/log/nginx/access.log
RUN touch /var/log/nginx/error.log
