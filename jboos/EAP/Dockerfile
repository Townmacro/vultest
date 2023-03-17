FROM jboss/base-jdk:8

# Set the JBOSS_VERSION env variable
ENV JBOSS_HOME /opt/jboss/jboss-as-6.1
ENV EAP_HOME /opt/jboss/jboss-as-6.1

# Add the JBoss distribution to /opt, and make jboss the owner of the extracted zip content
# https://jbossas.jboss.org/downloads 
RUN curl https://download.jboss.org/jbossas/6.1/jboss-as-distribution-6.1.0.Final.zip -o /opt/jboss/jboss-as-6.1.0.zip
RUN jar -xvf /opt/jboss/jboss-as-6.1.0.zip \
&& mv /opt/jboss/jboss-6.1.0.Final $EAP_HOME \
&& chmod a+x $EAP_HOME/bin/*

# Ensure signals are forwarded to the JVM process correctly for graceful shutdown
#ENV LAUNCH_JBOSS_IN_BACKGROUND true

# Enable binding to all network interfaces and debugging inside the EAP
RUN echo "JAVA_OPTS=\"\$JAVA_OPTS -Djboss.bind.address=0.0.0.0 -Djboss.bind.address.management=0.0.0.0\"" >> ${EAP_HOME}/bin/run.conf

# Expose the ports we're interested in
EXPOSE 8080 9990 4447 9999 4446 3873 4445

# Set the default command to run on boot
# This will boot JBoss EAP in the standalone mode and bind to all interface
ENTRYPOINT ["/opt/jboss/jboss-as-6.1/bin/run.sh"]
