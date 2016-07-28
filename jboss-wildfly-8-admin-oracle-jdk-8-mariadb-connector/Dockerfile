FROM koenigsflieger/jboss-wildfly-8-oracle-jdk-8

USER root

# Install MariaDB-Client from repository.
RUN add-apt-repository -y 'deb http://ftp.osuosl.org/pub/mariadb/repo/5.5/ubuntu trusty main' \
    && apt-get update \
    && DEBIAN_FRONTEND=noninteractive apt-get install -y --force-yes mariadb-client

# switch to wildfly
USER wildfly

# add mariadb-connector
# COPY org /opt/jboss/wildfly/modules/org/
COPY com /opt/jboss/wildfly/modules/com/

#add mariaDB-Driver to configuration
#<driver name="mariadb" module="com.mariadb">
# <xa-datasource-class>org.mariadb.jdbc.MySQLDataSource</xa-datasource-class>
#</driver>
COPY conf /opt/jboss/wildfly/standalone/configuration/

# add user admin with pwd admin
RUN /opt/jboss/wildfly/bin/add-user.sh admin admin --silent

