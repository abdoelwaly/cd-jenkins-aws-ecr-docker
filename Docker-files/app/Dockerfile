FROM maven:3.9.9-eclipse-temurin-21-jammy AS BUILD_IMAGE
RUN git clone https://github.com/abdoelwaly/poc-projects.git
RUN cd poc-projects && git checkout containers && mvn install



FROM tomcat:10-jdk21
LABEL "projects"="poc"
LABEL "Author"="abdoelwaly"
RUN rm -rf /usr/local/tomcat/webapps/*
COPY --from=BUILD_IMAGE poc-projects/target/profile-v2.war usr/local/tomcat/webapps/ROOT.war

EXPOSE 8080
CMD [ "catlina.sh", "run" ]

# have multistage image to reduce the size of the tomact image, so we run first container BUILD_IMAGE and copied to tomcat image 