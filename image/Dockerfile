FROM nginx:stable-alpine


RUN apk update && apk add npm && \
        npm install -g sass
COPY ./404 /usr/share/nginx/html
RUN sass /usr/share/nginx/html/style.scss /usr/share/nginx/html/style.css
CMD ["nginx", "-g", "daemon off;"]
