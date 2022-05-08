FROM debian

# COPY ./404 /usr/share/nginx/html
RUN apt-get update && apt-get install npm && \
        npm install -g sass
RUN sass /usr/share/nginx/html/style.scss /usr/share/nginx/html/style.css
