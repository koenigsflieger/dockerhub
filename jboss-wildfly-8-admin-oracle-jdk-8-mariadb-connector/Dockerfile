FROM koenigsflieger/jboss-wildfly-8-oracle-jdk-8

# Install MariaDB-Client from repository.
# ADD apt-sources.list.d /etc/apt/sources.list.d/

USER root

RUN \
    add-apt-repository -y 'deb http://ftp.osuosl.org/pub/mariadb/repo/5.5/ubuntu trusty main' && \
    apt-get update && \
    DEBIAN_FRONTEND=noninteractive apt-get install -y --force-yes mariadb-client

# RUN sudo apt-get update && sudo apt-get install mariadb-client -y
# RUN apt-get update && apt-get install -y --force-yes mariadb-client

USER wildfly

# add mariadb-connector
# ADD org /opt/jboss/wildfly/modules/org/
ADD com /opt/jboss/wildfly/modules/com/

#add mariaDB-Driver to configuration
#<driver name="mariadb" module="com.mariadb">
# <xa-datasource-class>org.mariadb.jdbc.MySQLDataSource</xa-datasource-class>
#</driver>
ADD conf /opt/jboss/wildfly/standalone/configuration/

# add user admin with pwd admin
RUN /opt/jboss/wildfly/bin/add-user.sh admin admin --silent

