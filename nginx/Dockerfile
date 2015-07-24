FROM nginx

RUN cd /etc/nginx/conf.d \
  && rm -rf * \
  && echo "alias ll='ls -l'" >> /root/.bashrc

COPY assets/default.conf /etc/nginx/conf.d/default.conf
