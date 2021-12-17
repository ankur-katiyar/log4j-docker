FROM jamesdbloom/docker-java8-maven as maven_builder
ENV JAVA_HOME=/usr/lib/jvm/java-8-openjdk-amd64/jre
RUN mkdir -p /app
WORKDIR /app/
RUN git clone https://github.com/ankur-katiyar/log4j-vunerable-server.git
WORKDIR /app/log4j-vunerable-server/
RUN mvn clean install 

#FROM tomcat:8.5.43-jdk8
FROM tomcat:8.0.53-jre8
COPY --from=maven_builder /app/log4j-vunerable-server/target/Test.war /usr/local/tomcat/webapps
