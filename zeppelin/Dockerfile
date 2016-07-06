# docker build . -t centos6:zeppelin
# docker run -i -P -v $(pwd)/share:/opt/share centos6:zeppelin

FROM centos:centos6

ENV JAVA_HOME=/opt/jdk1.8.0_91 \
  MVN_HOME=/opt/apache-maven-3.3.9

# fontconfig was required because phantomJS
# wouldn't run without it when building zeppelin

RUN yum install -y wget \
  && yum install -y git
RUN cd /opt \
  && wget --no-cookies --no-check-certificate --header "Cookie: gpw_e24=http%3A%2F%2Fwww.oracle.com%2F; oraclelicense=accept-securebackup-cookie" "http://download.oracle.com/otn-pub/java/jdk/8u91-b14/jdk-8u91-linux-x64.tar.gz" \
  && tar xzf jdk-8u91-linux-x64.tar.gz
RUN cd /opt \
  && wget "http://apache.mirrors.lucidnetworks.net/maven/maven-3/3.3.9/binaries/apache-maven-3.3.9-bin.tar.gz" \
  && tar xvf apache-maven-3.3.9-bin.tar.gz \
  && wget "http://mirrors.sonic.net/apache/incubator/zeppelin/0.5.6-incubating/zeppelin-0.5.6-incubating.tgz" \
  && tar xvf zeppelin-0.5.6-incubating.tgz
RUN cd ~ \
  && echo "" >> ~/.bashrc \
  && echo "export PATH=$JAVA_HOME/bin:$MVN_HOME/bin:$PATH" >> ~/.bashrc \
  && echo "" >> ~/.bashrc
# RUN curl --silent --location https://rpm.nodesource.com/setup | bash - \
#  && yum -y install nodejs \
#  && yum -y install npm
# RUN wget http://download.fedoraproject.org/pub/epel/6/x86_64/epel-release-6-8.noarch.rpm \
#  && rpm -ivh epel-release-6-8.noarch.rpm \
#  && yum -y install fontconfig --enablerepo=epel

COPY ./settings.xml /root/.m2

# Default command
CMD ["/bin/bash"]
