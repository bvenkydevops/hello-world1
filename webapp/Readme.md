----------------------------------------------------------
**NORMAL DOCKERFILE OR Single stage Dockerfile**
----------------------------------------------------------







----------------------------------------------
#docker build -t javawebapp .
root@ip-172-31-86-113:~/hello-world1/webapp# docker images
    REPOSITORY             TAG            IMAGE ID       CREATED          SIZE
--> javawebapp            latest       a3aa4b21321c   23 minutes ago   **961MB** 

 #docker run --name c1 -d -p 8080:8080 javawebapp:latest
      d79f3a4b258016deb938af7f254d5c4ff1ad3b4535c99d5818b4448938dd982b
## ACCESS the container in browser using
# http://3.94.105.153:8080/webapp/

![Screenshot (444)](https://github.com/user-attachments/assets/3e7f6e6a-8085-4101-a34e-33ec633f928f)


# HERE ,see the above Normal Dockerfile when the build image, the Docker image Size is **962MB**
# So, I want to reduce my docker image size for that,


--------------------------------------------------------------------------------------------------------------------------------
# Multistage Docker file ,In this 2 stages are there 1 .Build stage 2.Final stage
---------------------------------------------------------------------------------------------------------------------------------
################## Build stage #################################################
# Use Ubuntu as the base image for building the app
FROM ubuntu:20.04 AS build
ENV DEBIAN_FRONTEND=noninteractive
# Install Java 17 and Maven
RUN apt-get update && \
    apt-get install -y openjdk-17-jdk maven git

# Clone the repository
RUN git clone https://github.com/bvenkydevops/hello-world1.git

# Set the working directory to the webapp folder
WORKDIR /hello-world1/webapp

# Build the project using Maven
RUN mvn clean package
###################### Final stage #############################
# Use a new image for deployment with Tomcat
FROM tomcat:9.0.76-jdk17

# Copy the WAR file from the build stage to Tomcat's webapps directory
COPY --from=build /hello-world1/webapp/target/*.war /usr/local/tomcat/webapps/

# Expose port 8080
EXPOSE 8080

# Start Tomcat
CMD ["catalina.sh", "run"]
------------------------------------------------------------------------------------
#docker build -t javawebappmultistage .
root@ip-172-31-86-113:~/hello-worldld1/webapp# docker images
    REPOSITORY             TAG            IMAGE ID       CREATED          SIZE
--> javawebappmultistage   latest         2eb3e8681d04   11 seconds ago   **476MB**

 #docker run --name c1 -d -p 8080:8080 jjavawebappmultistage:latest
      cacc217a58f703b60232df314aaae48dfc253ea7d5a4b45167a60e8f4a0a3651
![Screenshot (448)](https://github.com/user-attachments/assets/8e614c44-e52f-413a-8ec2-9d7e7936c8cc)

 # see the Difference Docker image size after using multistage Dockerfile   
![Screenshot (447)](https://github.com/user-attachments/assets/6af81592-a2cd-4f61-a2d6-f6ca0c4481bb)

      

