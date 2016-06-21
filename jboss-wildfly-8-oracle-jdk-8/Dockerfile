FROM ubuntu:14.04

RUN sudo /bin/sh -c 'apt-get update && apt-get install software-properties-common python-software-properties -y'

RUN sudo /bin/sh -c 'apt-get update && sudo add-apt-repository ppa:webupd8team/java'

RUN sudo /bin/sh -c 'echo oracle-java8-installer shared/accepted-oracle-license-v1-1 select true | sudo /usr/bin/debconf-set-selections && apt-get install oracle-java8-set-default oracle-java8-installer -y'

# Set the WILDFLY_VERSION env variable
ENV WILDFLY_VERSION 8.2.0.Final

# Add the WildFly distribution to /opt/jboss
RUN mkdir /opt/jboss
RUN cd /opt/jboss && wget http://download.jboss.org/wildfly/$WILDFLY_VERSION/wildfly-$WILDFLY_VERSION.tar.gz
RUN cd /opt/jboss && tar xvf wildfly-$WILDFLY_VERSION.tar.gz && rm wildfly-$WILDFLY_VERSION.tar.gz

# Make sure the distribution is available from a well-known place
RUN ln -s /opt/jboss/wildfly-$WILDFLY_VERSION /opt/jboss/wildfly

# Set the JBOSS_HOME env variable
ENV JBOSS_HOME /opt/jboss/wildfly

# Create a user and group used to launch processes
# The user ID 1000 is the default for the first "regular" user on Fedora/RHEL,
# so there is a high chance that this ID will be equal to the current user
# making it easier to use volumes (no permission issues)
RUN groupadd -r wildfly -g 1000 && useradd -u 1000 -r -g wildfly -d /opt/jboss/wildfly -s /bin/false -c "WildFly user" wildfly

# Change the owner of the /opt/jboss/wildfly directory
RUN chown -R wildfly:wildfly /opt/jboss/wildfly*

# Expose the ports we're interested in
EXPOSE 8080 9990

# Run everything below as the wildfly user
USER wildfly

# Set the default command to run on boot
# This will boot WildFly in the standalone mode and bind to all interface
CMD ["/opt/jboss/wildfly/bin/standalone.sh", "-b", "0.0.0.0", "-bmanagement", "0.0.0.0"]