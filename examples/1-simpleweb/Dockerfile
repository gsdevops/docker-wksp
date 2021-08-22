FROM nginx

#COPY /usr/share/kpep/ /usr/share/nginx/html/
COPY /html/ /usr/share/nginx/html/
ADD https://www.google.com/ /usr/share/nginx/html/2.html
EXPOSE 80
RUN ls -la /usr/share/nginx/html/ &&   \ 
    chmod a+r /usr/share/nginx/html/2.html && \
     sleep 2

#docker build -t simpleweb .
#docler run -it -p 8000:80 simpleweb
