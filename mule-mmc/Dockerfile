# Dockerizing Mule MMC
# Version:  0.1
# Based on:  dockerfile/java (Trusted Java from http://java.com)

FROM                    java:latest
MAINTAINER              Conrad Pöpke <conrad@poepke.info>

# Mule MMC installation:

# This line can reference either a web url (ADD), network share or local file (COPY)
COPY                    ./mmc-distribution-mule-console-bundle-3.7.0.zip /opt/

WORKDIR                 /opt
RUN                     echo "6f8765ba1baddf27ac2212110a2a33a1 mmc-distribution-mule-console-bundle-3.7.0.zip" | md5sum -c
RUN                     unzip /opt/mmc-distribution-mule-console-bundle-3.7.0.zip
RUN                     ln -s mmc-distribution-mule-console-bundle-3.7.0/mmc-3.7.0/apache-tomcat-7.0.52 mmc
RUN                     rm -f  mmc-distribution-mule-console-bundle-3.7.0.zip

# Remove things that we don't need in production:
RUN                     rm -Rf mmc-distribution-mule-console-bundle-3.7.0/mule-enterprise-3.7.0
RUN                     rm -f mmc-distribution-mule-console-bundle-3.7.0/startup*
RUN                     rm -f mmc-distribution-mule-console-bundle-3.7.0/shutdown*
RUN                     rm -f mmc-distribution-mule-console-bundle-3.7.0/status*
RUN                     rm -Rf mmc-distribution-mule-console-bundle-3.7.0/mmc-3.7.0/apache-tomcat-7.0.52/webapps/examples
RUN                     rm -Rf mmc-distribution-mule-console-bundle-3.7.0/mmc-3.7.0/apache-tomcat-7.0.52/webapps/host-manager
RUN                     rm -Rf mmc-distribution-mule-console-bundle-3.7.0/mmc-3.7.0/apache-tomcat-7.0.52/webapps/docs
RUN                     rm -Rf mmc-distribution-mule-console-bundle-3.7.0/mmc-3.7.0/apache-tomcat-7.0.52/webapps/manager
RUN                     rm -Rf mmc-distribution-mule-console-bundle-3.7.0/mmc-3.7.0/apache-tomcat-7.0.52/webapps/ROOT/*

# Configure external access:

# Mule remote debugger
EXPOSE  5000

# Mule JMX port (must match Mule config file)
EXPOSE  1098

# Mule MMC port
EXPOSE  8585

# Environment and execution:

CMD             /opt/mmc/bin/startup.sh && tail -f /opt/mmc/logs/catalina.out