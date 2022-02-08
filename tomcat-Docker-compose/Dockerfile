# Installing OS
FROM centos:7

# Installing Java
ENV JAVA_HOME=/apps/tomcat/java/current
ENV PATH=$PATH:$JAVA_HOME
RUN yum install java-1.8.0-openjdk-devel wget -y
EXPOSE 8080

# Installing and configuring Tomcat
ENV Tomcat_Version=9.0.54
RUN 	wget http://www-eu.apache.org/dist/tomcat/tomcat-9/v${Tomcat_Version}/bin/apache-tomcat-${Tomcat_Version}.tar.gz && \
	tar xvfz apache-tomcat-${Tomcat_Version}.tar.gz && \
        mkdir -p /apps/tomcat/uat/ /apps/tomcat/java/java-1.8.0-openjdk && \
	mv apache-tomcat-${Tomcat_Version}.tar.gz /tmp/ && \
	mv apache-tomcat-${Tomcat_Version}/* /apps/tomcat/uat/. && \
	cp -r /usr/lib/jvm/java-1.8.0-openjdk/* /apps/tomcat/java/java-1.8.0-openjdk/ && \
	ln -s /apps/tomcat/java/java-1.8.0-openjdk /apps/tomcat/java/current
COPY ${PWD}/conf/context.xml /apps/tomcat/uat/conf/
COPY ${PWD}/conf/tomcat-users.xml /apps/tomcat/uat/conf/
COPY ${PWD}/conf/server.xml /apps/tomcat/uat/conf/
COPY ${PWD}/ROOT /apps/tomcat/uat/webapps/ROOT
COPY ${PWD}/conf/context.xml /apps/tomcat/uat/webapps/manager/META-INF/
CMD ["/apps/tomcat/uat/bin/catalina.sh", "run"]
