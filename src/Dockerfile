FROM nginx
RUN mkdir -p /payload
RUN echo "Jugurtha" >> /usr/share/nginx/html/index.html
RUN ls -alt 
COPY target/*.jar /payload/
