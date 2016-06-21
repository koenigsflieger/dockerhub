FROM koenigsflieger/jboss-wildfly-8-oracle-jdk-8

# Install MariaDB-Client from repository.
ADD apt-sources.list.d /etc/apt/sources.list.d/
#RUN sudo apt-get update && DEBIAN_FRONTEND=noninteractive apt-get install -y --force-yes mariadb-client
RUN sudo apt-get update && sudo apt-get install -y --force-yes mariadb-client
# RUN apt-get update && apt-get install -y --force-yes mariadb-client

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

