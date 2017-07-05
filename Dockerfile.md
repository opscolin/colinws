FROM centos:7
ENV CATALINA_HOME /usr/local/tomcat
RUN	rpm -ivh https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm && \
	yum install wget tar -y && \
	rpm -ivh http://www.yijianhuashi.com/jdk-8u91-linux-x64.rpm && \
	wget http://www.yijianhuashi.com/tomcat-service.tar.gz && \
	tar -zxf tomcat-service.tar.gz -C /usr/local/ && useradd tomcat && chown -R tomcat:tomcat /usr/local/tomcat && \
	sed -i '$aJAVA_HOME=/usr/java/default\nPATH=$PATH:$JAVA_HOME/bin\nexport PATH JAVA_HOME' /etc/profile && source /etc/profile && yum clean all
EXPOSE 8080 9094
ENTRYPOINT ["su tomcat /usr/local/tomcat/bin/tomcat", "start"]
