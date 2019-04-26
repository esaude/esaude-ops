# adapted from:
# https://github.com/pgracio/dhis2-docker

FROM tomcat:7-jre8

ADD hibernate.properties /opt/dhis2/config/hibernate.properties
ADD dhis.conf /opt/dhis2/config/dhis.conf
ADD wait-for-it.sh wait-for-it.sh

RUN mkdir -p /opt/dhis2/config \
    && echo "export DHIS2_HOME='/opt/dhis2/config'" >> /usr/local/tomcat/bin/setenv.sh \
    && wget https://www.dhis2.org/download/releases/2.20/dhis.war \
    && rm -fR /usr/local/tomcat/webapps/ROOT \
    && mv dhis.war /usr/local/tomcat/webapps/ROOT.war

EXPOSE 8080
