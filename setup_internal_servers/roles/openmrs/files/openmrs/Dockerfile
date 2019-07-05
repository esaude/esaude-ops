FROM alpine AS build

RUN apk update && apk add curl unzip; \
  curl -L http://sourceforge.net/projects/openmrs/files/releases/OpenMRS_Platform_1.11.7/openmrs.war/download \
  -o /openmrs.war;


FROM tomcat:7-jre7-alpine

ARG DB_HOST="mysql-db"
ARG DB_DATABASE="openmrs"
ARG DB_USERNAME="openmrs"
ARG DB_PASSWORD="openmrs"
ARG DB_AUTO_UPDATE="false"

ADD openmrs-runtime.properties /usr/local/tomcat/openmrs-runtime.properties
ADD setenv.sh /usr/local/tomcat/bin/setenv.sh

RUN sed -i "s|@DB_HOST@|$DB_HOST|g" /usr/local/tomcat/openmrs-runtime.properties; \
  sed -i "s|@DB_DATABASE@|$DB_DATABASE|g" /usr/local/tomcat/openmrs-runtime.properties; \
  sed -i "s|@DB_USERNAME@|$DB_USERNAME|g" /usr/local/tomcat/openmrs-runtime.properties; \
  sed -i "s|@DB_PASSWORD@|$DB_PASSWORD|g" /usr/local/tomcat/openmrs-runtime.properties; \
  sed -i "s|@DB_AUTO_UPDATE@|$DB_AUTO_UPDATE|g" /usr/local/tomcat/openmrs-runtime.properties;

COPY --from=build /openmrs.war /usr/local/tomcat/webapps/openmrs.war
