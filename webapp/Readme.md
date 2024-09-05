docker build -t javawebapp .
 docker run --name c1 -d -p 8080:8080 javawebapp:latest
d79f3a4b258016deb938af7f254d5c4ff1ad3b4535c99d5818b4448938dd982b


root@ip-172-31-86-113:~/hello-world1/webapp# docker ps
CONTAINER ID   IMAGE               COMMAND                  CREATED         STATUS         PORTS                                       NAMES
d79f3a4b2580   javawebapp:latest   "/usr/local/tomcat/b…"   7 seconds ago   Up 7 seconds   0.0.0.0:8080->8080/tcp, :::8080->8080/tcp   c1

## ACCESS the container in browser using
# http://3.94.105.153:8080/webapp/

![Screenshot (444)](https://github.com/user-attachments/assets/3e7f6e6a-8085-4101-a34e-33ec633f928f)
