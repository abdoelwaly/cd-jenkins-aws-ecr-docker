FROM nginx
LABEL "projects"="poc"
LABEL "Author"="abdoelwaly"


RUN rm -rf /etc/nginx/conf.d/default.conf
COPY nginpocapp.conf /etc/nginx/conf.d/pocapp.conf