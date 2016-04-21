FROM koenigsflieger/jboss-wildfly-8-oracle-jdk-8

# add mariadb-connector
# ADD org /opt/jboss/wildfly/modules/org/
ADD com /opt/jboss/wildfly/modules/com/

# add user admin with pwd admin
RUN /opt/jboss/wildfly/bin/add-user.sh admin admin --silent

